<h1>ExpNo 2 : Implement Depth First Search Traversal of a Graph</h1> 
<h3>Name: </h3>
<h3>Register Number:     </h3>
<H3>Aim:</H3>
<p> To Implement Depth First Search Traversal of a Graph using Python 3.</p>
<h3>Theory:</h3>
<strong>Depth First Traversal </strong>(or DFS) for a graph is like Depth First Traversal of a tree. The only catch here is that, unlike trees, graphs may contain cycles (a node may be visited twice). Use a Boolean visited array to avoid processing a node more than once. A graph can have more than one DFS traversal. 
Depth-first search is an algorithm for traversing or searching trees or graph data structures. The algorithm starts at the root node (selecting some arbitrary node as the root node in the case of a graph) and explores as far as possible along each branch before backtracking.
Step 1: Initially, stack and visited arrays are empty.

 ![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/640b3c6f-3ac1-49a2-a955-68da9a71f446)


Queue and visited arrays are empty initially.
Stack and visited arrays are empty initially.
Step 2: Visit 0 and put its adjacent nodes which are not visited yet into the stack.
 ![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/86dcf7d9-1f9d-49b0-a821-5976a6e77606)

 Visit node 0 and put its adjacent nodes (1, 2, 3) into the stack
 Visit node 0 and put its adjacent nodes (1, 2, 3) into the stack

Step 3: Now, Node 1 at the top of the stack, so visit node 1 and pop it from the stack and put all of its adjacent nodes which are not visited in the stack.
 ![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/e6017942-08b1-4742-87ad-c97eb97bf985)

Visit node 1
 Visit node 1

Step 4: Now, Node 2 at the top of the stack, so visit node 2 and pop it from the stack and put all of its adjacent nodes which are not visited (i.e, 3, 4) in the stack.
 ![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/6e6d123c-60ae-4f9c-a27c-c4fc7e57d57c)

 Visit node 2 and put its unvisited adjacent nodes (3, 4) into the stack
 Visit node 2 and put its unvisited adjacent nodes (3, 4) into the stack

Step 5: Now, Node 4 at the top of the stack, so visit node 4 and pop it from the stack and put all of its adjacent nodes which are not visited in the stack.
 ![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/20b76a05-5668-4da5-8189-e10fb1bb7238)

 Visit node 4
 Visit node 4

Step 6: Now, Node 3 at the top of the stack, so visit node 3 and pop it from the stack and put all of its adjacent nodes which are not visited in the stack.
 ![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/3b88f04a-7846-4f75-89b4-22bbd5b48e52)

Visit node 3
Visit node 3

Now, the Stack becomes empty, which means we have visited all the nodes, and our DFS traversal ends.

<h3>Algorithm:</h3>
<B><ol>
 <li>Construct a Graph with Nodes and Edges</li>
 <li>Depth First Search Uses Stack and Recursion</li>
 <li>Insert a START node to the STACK</li>
 <li>Find its Successors Or neighbors and Check whether the node is visited or not</li>
 <li>If Not Visited, add it to the STACK. Else Call The Function Again Until No more nodes needs to be visited.</li>
</ol></B>

<hr>
<h3>Sample Input</h3>
<hr>
8 9 <BR>
A B <BR>
A C <BR>
B E <BR>
C D <BR>
B D <BR>
C G <BR>
D F <BR>
G F <BR>
F H <BR>
<hr>
<h3>Sample Output</h3>
<hr>
['A', 'B', 'E', 'D', 'C', 'G', 'F', 'H']

<hr>
~~~

~~~
<!DOCTYPE html>
<html>
<head>
    <title>Graph DFS Visualization</title>
    <style>
        body {
            font-family: Arial;
            background-color: #f0f4f8;
            text-align: center;
            padding: 20px;
        }

        .container {
            background: white;
            padding: 25px;
            width: 500px;
            margin: auto;
            border-radius: 10px;
            box-shadow: 0 0 10px gray;
        }

        input, button {
            padding: 10px;
            margin: 8px;
            border-radius: 5px;
        }

        button {
            background-color: #007bff;
            color: white;
            border: none;
            cursor: pointer;
        }

        canvas {
            margin-top: 20px;
            border: 1px solid gray;
            background: #fafafa;
        }

        #result {
            font-weight: bold;
            color: green;
        }
    </style>
</head>
~~~
~~~
<body>

<div class="container">
    <h2>Graph DFS Visualization</h2>

    <label>Number of Nodes:</label><br>
    <input type="number" id="nodes" min="1"><br>

    <label>Number of Edges:</label><br>
    <input type="number" id="edges" min="0"><br>

    <label>Enter Edges (Example: A B):</label><br>
    <textarea id="edgeList" rows="5"
        placeholder="A B&#10;A C&#10;B D"></textarea><br>

    <label>Starting Node:</label><br>
    <input type="text" id="start" placeholder="Enter start node"><br>

    <button onclick="runDFS()">Generate Graph & DFS</button>

    <h3>Graph:</h3>
    <canvas id="graphCanvas" width="450" height="300"></canvas>

    <h3>DFS Result:</h3>
    <p id="result"></p>
</div>
~~~
~~~
<script>
function runDFS() {
    const nodes = parseInt(document.getElementById("nodes").value);
    const edges = parseInt(document.getElementById("edges").value);
    const edgeInput = document.getElementById("edgeList").value.trim();
    const start = document.getElementById("start").value.trim();

    if (!Number.isInteger(nodes) || nodes < 1 ||
        !Number.isInteger(edges) || edges < 0 ||
        !start || (edges > 0 && !edgeInput)) {
        alert("Please enter valid inputs!");
        return;
    }

    const graph = {};
    const allNodes = new Set();

    if (edges > 0) {
        const lines = edgeInput.split("\n")
            .map(line => line.trim())
            .filter(line => line.length > 0);

        if (lines.length !== edges) {
            alert("Number of edges does not match!");
            return;
        }

        for (let line of lines) {
            const parts = line.split(/\s+/);

            if (parts.length !== 2) {
                alert("Enter each edge as: A B");
                return;
            }

            const [u, v] = parts;

            allNodes.add(u);
            allNodes.add(v);

            if (!graph[u]) graph[u] = [];
            if (!graph[v]) graph[v] = [];

            graph[u].push(v);
            graph[v].push(u);
        }
    }

    if (allNodes.size > nodes) {
        alert("Number of unique nodes exceeds the given count!");
        return;
    }

    if (!allNodes.has(start)) {
        document.getElementById("result").innerText =
            "Starting node not found!";
        drawGraph(graph);
        return;
    }

    // Depth First Search
    const visited = new Set();
    const path = [];

    function dfs(node) {
        visited.add(node);
        path.push(node);

        for (let neighbour of graph[node]) {
            if (!visited.has(neighbour)) {
                dfs(neighbour);
            }
        }
    }

    dfs(start);

    document.getElementById("result").innerText =
        "DFS Traversal: " + path.join(" → ");

    document.getElementById("graphCanvas").style.display = "block";
    drawGraph(graph);
}

function drawGraph(graph) {
    const canvas = document.getElementById("graphCanvas");
    const ctx = canvas.getContext("2d");

    ctx.clearRect(0, 0, canvas.width, canvas.height);

    const nodes = Object.keys(graph);
    const centerX = canvas.width / 2;
    const centerY = canvas.height / 2;
    const radius = 110;
    const positions = {};

    nodes.forEach((node, i) => {
        const angle = (2 * Math.PI * i) / nodes.length;
        positions[node] = {
            x: centerX + radius * Math.cos(angle),
            y: centerY + radius * Math.sin(angle)
        };
    });
~~~

    ctx.strokeStyle = "red";
    ctx.lineWidth = 2;

    const drawn = new Set();

    nodes.forEach(node => {
        graph[node].forEach(neighbour => {
            const key = [node, neighbour].sort().join("-");
            if (drawn.has(key)) return;
            drawn.add(key);

            ctx.beginPath();
            ctx.moveTo(positions[node].x, positions[node].y);
            ctx.lineTo(positions[neighbour].x, positions[neighbour].y);
            ctx.stroke();
        });
    });
~~~
~~~
    // Draw nodes
    nodes.forEach(node => {
        const { x, y } = positions[node];

        ctx.beginPath();
        ctx.arc(x, y, 20, 0, 2 * Math.PI);
        ctx.fillStyle = "lightblue";
        ctx.fill();
        ctx.strokeStyle = "black";
        ctx.stroke();

        ctx.fillStyle = "black";
        ctx.textAlign = "center";
        ctx.textBaseline = "middle";
        ctx.fillText(node, x, y);
    });
}
~~~
</script>

</body>
</html>

~~~
~~~


<hr>
<h3>Sample Input</h3>
<hr>
5 5 <BR>
0 1 <BR>
0 2 <BR>
0 3 <BR>
2 3 <BR>
2 4 <BR>
<hr>
<h3>Sample Output</h3>
<hr>
['0', '1', '2', '3', '4']

<hr>
<h3>Result:</h3>
<hr>
<p>Thus,a Graph was constructed and implementation of Depth First Search for the same graph was done successfully.</p>

##output:

<img width="862" height="900" alt="image" src="https://github.com/user-attachments/assets/90d5af32-4947-4f9a-81cf-b09d960b06df" />
