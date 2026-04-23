<html>
<head>
    <title>Call Center Management</title>
    <style>
        body {
            font-family: Arial;
            background: #f4f4f4;
            padding: 20px;
        }
        h1 {
            text-align: center;
        }
        .form {
            background: white;
            padding: 15px;
            border-radius: 10px;
            width: 300px;
            margin: auto;
        }
        input, select, button {
            width: 100%;
            margin: 5px 0;
            padding: 8px;
        }
        table {
            width: 80%;
            margin: 20px auto;
            border-collapse: collapse;
        }
        th, td {
            border: 1px solid gray;
            padding: 10px;
            text-align: center;
        }
        th {
            background: #333;
            color: white;
        }
    </style>
</head>

<body>

<h1>📞 Call Center Management System</h1>

<div class="form">
    <input type="text" id="customer" placeholder="Customer Name">
    <input type="text" id="issue" placeholder="Issue">
    
    <select id="agent">
        <option value="">Select Agent</option>
        <option>Agent A</option>
        <option>Agent B</option>
        <option>Agent C</option>
    </select>

    <button onclick="addCall()">Add Call</button>
</div>

<table>
    <thead>
        <tr>
            <th>Customer</th>
            <th>Issue</th>
            <th>Agent</th>
            <th>Status</th>
            <th>Action</th>
        </tr>
    </thead>
    <tbody id="callList"></tbody>
</table>

<script>
    let calls = [];

    function addCall() {
        let customer = document.getElementById("customer").value;
        let issue = document.getElementById("issue").value;
        let agent = document.getElementById("agent").value;

        if (customer === "" || issue === "" || agent === "") {
            alert("Please fill all fields");
            return;
        }

        let call = {
            customer,
            issue,
            agent,
            status: "Pending"
        };

        calls.push(call);
        displayCalls();

        // clear fields
        document.getElementById("customer").value = "";
        document.getElementById("issue").value = "";
        document.getElementById("agent").value = "";
    }

    function displayCalls() {
        let table = document.getElementById("callList");
        table.innerHTML = "";

        calls.forEach((call, index) => {
            table.innerHTML += `
                <tr>
                    <td>${call.customer}</td>
                    <td>${call.issue}</td>
                    <td>${call.agent}</td>
                    <td>${call.status}</td>
                    <td>
                        <button onclick="completeCall(${index})">Complete</button>
                        <button onclick="deleteCall(${index})">Delete</button>
                    </td>
                </tr>
            `;
        });
    }

    function completeCall(index) {
        calls[index].status = "Completed";
        displayCalls();
    }

    function deleteCall(index) {
        calls.splice(index, 1);
        displayCalls();
    }
</script>

</body>
</html>
