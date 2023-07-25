# SNwatchdog
Watching SN that are online or offline
Set Up HTML Structure: Create the basic HTML structure for your webpage. Include a container to hold the node status information.
html
Copy code
<!DOCTYPE html>
<html>
<head>
    <title>Graft Service Nodes Status</title>
</head>
<body>
    <h1>Graft Service Nodes Status</h1>
    <div id="nodeStatusContainer">
        <!-- Node status items will be dynamically added here -->
    </div>
</body>
</html>
Fetch Data with JavaScript: Use JavaScript to fetch the status data from the Graft API. You can use the Fetch API or other libraries like Axios to make the HTTP request.
html
Copy code
<script>
    // Function to fetch Graft Service Nodes status
    async function fetchNodesStatus() {
        try {
            const response = await fetch('https://api.example.com/graft-nodes-status');
            const data = await response.json();
            return data; // Assuming the API returns a JSON array of nodes with status information
        } catch (error) {
            console.error('Error fetching nodes status:', error);
            return [];
        }
    }
</script>
Display Status Data: Update the webpage with the retrieved node status data.
html
Copy code
<script>
    async function displayNodesStatus() {
        const nodeStatusContainer = document.getElementById('nodeStatusContainer');
        nodeStatusContainer.innerHTML = ''; // Clear existing node status items

        const nodesStatus = await fetchNodesStatus();

        nodesStatus.forEach(node => {
            const nodeItem = document.createElement('div');
            nodeItem.classList.add('node-status-item');

            const nodeName = document.createElement('span');
            nodeName.textContent = node.name;
            nodeItem.appendChild(nodeName);

            const nodeStatus = document.createElement('span');
            nodeStatus.textContent = node.online ? 'Online' : 'Offline';
            nodeStatus.classList.add(node.online ? 'online' : 'offline');
            nodeItem.appendChild(nodeStatus);

            const nodeAdditionalInfo = document.createElement('p');
            nodeAdditionalInfo.textContent = `Additional Info: ${node.additionalInfo}`;
            nodeItem.appendChild(nodeAdditionalInfo);

            nodeStatusContainer.appendChild(nodeItem);
        });
    }

    displayNodesStatus(); // Call the function to display nodes status initially
</script>
Style with CSS: Apply CSS styles to format the node status items.
html
Copy code
<style>
    h1 {
        text-align: center;
    }

    #nodeStatusContainer {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        gap: 20px;
    }

    .node-status-item {
        padding: 10px;
        border: 1px solid #ccc;
        width: 250px;
        text-align: center;
    }

    .online {
        color: green;
    }

    .offline {
        color: red;
    }
</style>
In this example, the JavaScript code fetches the Graft Service Nodes' status data from the specified API endpoint and then dynamically creates HTML elements to display the node names, online/offline status, and additional information for each node. The CSS styles add formatting to the node status items.

Please note that the provided JavaScript code assumes that the API returns a JSON array of nodes, and each node object contains properties like name, online, and additionalInfo. Replace 'https://api.example.com/graft-nodes-status' with the actual API endpoint that provides the Graft Service Nodes' status data. Also, adjust the code according to the structure of the API response.
