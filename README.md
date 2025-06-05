<%@ page language="java" contentType="text/html; charset=ISO-8859-1" pageEncoding="ISO-8859-1"%>
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
<!DOCTYPE html>
<html>
<head>
    <meta charset="ISO-8859-1">
    <title>Employee Report</title>

    <!-- Bootstrap CSS v5 -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">

    <style>
        /* Modal content style: rounded corners & soft shadow */
        #confirmDeleteModal .modal-content {
            border-radius: 12px;
            box-shadow: 0 6px 20px rgba(0, 0, 0, 0.12);
            background-color: white;
        }
        /* Center modal body text */
        #confirmDeleteModal .modal-body {
            text-align: center;
            font-size: 1rem;
        }
        /* Modal header: remove border & center title */
        #confirmDeleteModal .modal-header {
            border-bottom: none;
            justify-content: center;
        }
        #confirmDeleteModal .modal-title {
            margin: 0 auto;
        }
        /* Modal footer: center buttons & remove border */
        #confirmDeleteModal .modal-footer {
            justify-content: center;
            border-top: none;
        }
        /* Button rounded corners */
        .btn-outline-secondary {
            border-radius: 20px;
        }
        .btn-danger {
            border-radius: 20px;
        }
    </style>
</head>
<body>

<div class="container mt-4">
    <h3>Employee Report</h3>

    <a href="${pageContext.request.contextPath}/addEmployee" class="btn btn-primary mb-3">Add Employee</a>
    <a href="${pageContext.request.contextPath}/exportToCSV" class="btn btn-success mb-3">Export to CSV</a>

    <table class="table table-bordered">
        <thead>
            <tr>
                <th>ID</th>
                <th>Name</th>
                <th>Designation</th>
                <th>Department</th>
                <th>Salary</th>
                <th>Email</th>
                <th>Phone Number</th>
                <th>Address</th>
                <th>Actions</th>
            </tr>
        </thead>
        <tbody>
            <c:forEach var="emp" items="${employeeList}">
                <tr>
                    <td>${emp.id}</td>
                    <td>${emp.name}</td>
                    <td>${emp.designation}</td>
                    <td>${emp.department}</td>
                    <td>${emp.salary}</td>
                    <td>${emp.email}</td>
                    <td>${emp.phoneNumber}</td>
                    <td>${emp.address}</td>
                    <td>
                        <a href="${pageContext.request.contextPath}/editEmployee/${emp.id}" class="btn btn-primary btn-sm">Edit</a>
                        <button onclick="confirmDelete('${emp.id}')" class="btn btn-danger btn-sm">Delete</button>
                    </td>
                </tr>
            </c:forEach>
        </tbody>
    </table>
</div>

<!-- Confirmation Modal -->
<div class="modal fade" id="confirmDeleteModal" tabindex="-1" aria-labelledby="confirmModalLabel" aria-hidden="true" data-bs-backdrop="false">
    <div class="modal-dialog modal-dialog-centered">
        <div class="modal-content shadow">
            <div class="modal-header">
                <h5 class="modal-title" id="confirmModalLabel">Confirmation</h5>
                <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
            </div>
            <div class="modal-body">
                Are you sure you want to remove this element (ID: <span id="deleteEmployeeId" class="text-danger fw-bold"></span>)?
            </div>
            <div class="modal-footer">
                <button type="button" class="btn btn-outline-secondary" data-bs-dismiss="modal">Cancel</button>
                <button type="button" class="btn btn-danger" onclick="deleteEmployee()">Remove</button>
            </div>
        </div>
    </div>
</div>

<!-- Bootstrap JS Bundle -->
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>

<script>
    let selectedEmpId = null;

    function confirmDelete(id) {
        selectedEmpId = id;
        document.getElementById("deleteEmployeeId").innerText = id;

        // Show modal with no backdrop (no dark overlay)
        const modalElement = document.getElementById('confirmDeleteModal');
        const modal = new bootstrap.Modal(modalElement, {
            backdrop: false,
            keyboard: true
        });
        modal.show();
    }

    function deleteEmployee() {
        if (selectedEmpId) {
            window.location.href = '${pageContext.request.contextPath}/deleteEmployee/' + selectedEmpId;
        }
    }
</script>

</body>
</html>
