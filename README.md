<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KiranaKart POS</title>
    <style>
    body {
        background: #4B0082; /* Indigo background */
        margin: 0;
        padding: 0;
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        color: #333;
        min-height: 100vh;
        box-sizing: border-box;
    }

    .container {
        background: rgba(255, 255, 255, 0.95);
        padding: 30px;
        border-radius: 15px;
        box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
        width: 450px;
        max-width: 90%;
        text-align: center;
        display: none; /* Hidden by default since dashboard takes over */
        margin: 0 auto;
    }

    /* Feedback Button Styling (Top-Right Corner, below Support) */
    .feedback-btn {
        position: absolute;
        top: 20px; /* Positioned below the Support button */
        right: 110px;
        background: #2196F3; /* Blue background for visibility */
        color: white;
        padding: 10px 15px;
        border-radius: 50px;
        cursor: pointer;
        font-size: 14px;
        font-weight: bold;
        box-shadow: 0 3px 5px rgba(0, 0, 0, 0.2);
        transition: background 0.3s ease;
        z-index: 1000; /* Ensure it stays above other elements */
    }

    .feedback-btn:hover {
        background: #1976D2; /* Darker blue on hover */
    }

    h1 {
        color: #4b0082;
        margin-bottom: 25px;
        font-size: 28px;
        font-weight: 600;
    }

    .tabs {
        display: flex;
        justify-content: center;
        gap: 11px;
        margin-bottom: 20px;
    }

    .tab {
        padding: 12px 25px;
        cursor: pointer;
        background: #f0f0f0;
        border-radius: 25px;
        font-size: 16px;
        transition: all 0.3s ease;
    }

    .tab.active {
        background: #6a0dad;
        color: white;
        font-weight: 500;
    }

    .form-group {
        margin-bottom: 20px;
        text-align: left;
    }

    label {
        display: block;
        font-size: 14px;
        color: #555;
        margin-bottom: 8px;
    }

    input {
        width: 100%;
        padding: 12px;
        border: 2px solid #ddd;
        border-radius: 8px;
        font-size: 14px;
        box-sizing: border-box;
        transition: border-color 0.3s;
    }

    input:focus {
        border-color: #6a0dad;
        outline: none;
    }

    button {
        width: 100%;
        padding: 12px;
        border: none;
        border-radius: 8px;
        background: #6a0dad;
        color: white;
        font-size: 16px;
        cursor: pointer;
        transition: background 0.3s ease;
        -webkit-tap-highlight-color: transparent;
    }

    button:hover {
        background: #4b0082;
    }

    button:active {
        background: #4b0082;
    }

    .error {
        color: #d32f2f;
        background: #ffebee;
        padding: 10px;
        border-radius: 8px;
        display: none;
        margin-top: 10px;
        font-size: 14px;
    }

    .error.active {
        display: block;
    }

    #pos-dashboard {
        display: none;
        text-align: left;
        width: 100%;
        min-height: 100vh;
        background: white;
        padding: 25px;
        border: 4px solid;
        border-radius: 0;
        box-sizing: border-box;
        animation: borderAnimation 5s infinite;
        position: relative; /* For positioning the support button */
    }

    @keyframes borderAnimation {
        1% { border-color: #ff0000; }
        25% { border-color: #00ff00; }
        50% { border-color: #0000ff; }
        75% { border-color: #ffff00; }
        100% { border-color: #ff00ff; }
    }

    #pos-dashboard h2 {
        color: #4b0082;
        font-size: 30px;
        margin-bottom: 20px;
    }

    #pos-dashboard .dashboard-tabs {
        display: flex;
        gap: 108px;
        margin-bottom: 20px;
    }

    #pos-dashboard .item-form {
        display: grid;
        grid-template-columns: repeat(4, 1fr);
        gap: 25px;
        margin-bottom: 20px;
    }

    #pos-dashboard select, #pos-dashboard input[type="text"], #pos-dashboard input[type="number"], #pos-dashboard input[type="date"] {
        padding: 12px;
        border: 1px solid #ddd;
        border-radius: 100px;
        font-size: 18px;
    }

    #pos-dashboard .inventory-list, #pos-dashboard .stock-list {
        margin: 20px 0;
        max-height: 250px;
        overflow-y: auto;
        border: 1px solid #ddd;
        padding: 15px;
        background: #f9f9f9;
        border-radius: 8px;
    }

    /* Adjusted Inventory List Styling for Horizontal Layout */
    #pos-dashboard .inventory-list div {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 10px;
        font-size: 19px;
    }


#report-modal canvas {
    display: block;
    margin: 0 auto;
    border: 1px solid #ddd;
    border-radius: 10px;
}

#report-modal h4 {
    color: #4b0082;
    margin: 15px 0 10px;
    font-size: 16px;
}

#report-modal p {
    margin: 5px 0;
}

#report-modal ul li {
    margin: 5px 0;
    padding: 5px;
    background: #f9f9f9;
    border-radius: 5px;
}

#report-modal #sales-by-item p,
#report-modal #sales-trend p {
    margin: 5px 0;
    padding: 5px;
    background: #f0f0f0;
    border-radius: 5px;
}

/* Responsive adjustments for smaller screens */
@media only screen and (max-width: 600px) {
    #report-modal canvas {
        max-height: 150px;
    }

    #report-modal h4 {
        font-size: 14px;
    }

    #report-modal p,
    #report-modal ul li {
        font-size: 12px;
    }
}



    #pos-dashboard .inventory-list span {
        display: inline-block;
    }

    #pos-dashboard .inventory-list button {
        padding: 5px 10px;
        font-size: 12px;
        background: #6a0dad;
        color: white;
        border: none;
        border-radius: 5px;
        cursor: pointer;
        margin-right: 5px;
    }

    /* Adjusted Cart Item List Styling for Horizontal Layout */
    #pos-dashboard .item-list div {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 10px;
        font-size: 14px;
    }

    #pos-dashboard .item-list span {
        display: inline-block;
    }

    #pos-dashboard .item-list button {
        padding: 5px 10px;
        font-size: 12px;
        background: #d32f2f;
        color: white;
        border: none;
        border-radius: 5px;
        cursor: pointer;
        margin-left: 10px;
    }

    #pos-dashboard .stock-list p {
        margin: 28px 0;
        font-size: 19px;
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    #pos-dashboard .inventory-list button, #pos-dashboard .stock-list button {
        padding: 5px 10px;
        font-size: 20px;
        background: #6a0dad;
        color: white;
        border: none;
        border-radius: 25px;
        cursor: pointer;
        margin-left: 6px;
    }

    #pos-dashboard .inventory-list button:hover, #pos-dashboard .stock-list button:hover {
        background: #4b0082;
    }

    #pos-dashboard .modal {
        display: none;
        position: fixed;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        background: white;
        padding: 20px;
        border-radius: 10px;
        box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
        z-index: 1000;
        width: 500px;
        max-height: 80vh;
        overflow-y: auto;
    }

    #pos-dashboard .modal.active {
        display: block;
    }

    #pos-dashboard .modal h3 {
        color: #4b0082;
        margin-bottom: 15px;
        text-align: center;
    }

    #pos-dashboard .modal p {
        margin: 10px 0;
        font-size: 14px;
    }

    #pos-dashboard .modal ul {
        list-style: none;
        padding: 0;
        text-align: left;
    }

    #pos-dashboard .modal li {
        margin: 5px 0;
    }

    .dashboard-section {
        display: none;
    }

    .dashboard-section.active {
        display: block;
    }

    .quantity-modal {
        display: none;
        position: fixed;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        background: white;
        padding: 20px;
        border-radius: 10px;
        box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
        z-index: 1000;
        width: 300px;
    }

    .quantity-modal.active {
        display: block;
    }

    .quantity-modal h3 {
        color: #4b0082;
        margin-bottom: 15px;
    }

    .quantity-modal .form-group {
        margin-bottom: 15px;
    }

    .quantity-modal select {
        padding: 8px;
        border: 1px solid #ddd;
        border-radius: 5px;
        width: 100%;
    }

    .quantity-modal button {
        width: 48%;
        margin: 0 1%;
    }

    .stock-modal {
        display: none;
        position: fixed;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        background: white;
        padding: 20px;
        border-radius: 10px;
        box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
        z-index: 1000;
        width: 300px;
    }

    .stock-modal.active {
        display: block;
    }

    .stock-modal h3 {
        color: #4b0082;
        margin-bottom: 15px;
    }

    .invoice-header {
        text-align: center;
        border-bottom: 2px solid #4b0082;
        padding-bottom: 10px;
        margin-bottom: 20px;
    }

    .invoice-header h3 {
        margin: 0;
        font-size: 22px;
    }

    .invoice-details {
        display: flex;
        justify-content: space-between;
        margin-bottom: 20px;
    }

    .invoice-details p {
        margin: 5px 0;
    }

    .invoice-table {
        width: 100%;
        border-collapse: collapse;
        margin-bottom: 20px;
    }

    .invoice-table th, .invoice-table td {
        border: 1px solid #ddd;
        padding: 8px;
        text-align: left;
        font-size: 14px;
    }

    .invoice-table th {
        background-color: #f0f0f0;
        color: #4b0082;
    }

    /* Align numerical columns to the right in the invoice table */
    .invoice-table td:nth-child(2),
    .invoice-table td:nth-child(3),
    .invoice-table td:nth-child(4),
    .invoice-table td:nth-child(5),
    .invoice-table td:nth-child(6) {
        text-align: right;
    }

    .invoice-footer {
        text-align: right;
        border-top: 2px solid #4b0082;
        padding-top: 10px;
    }

    .invoice-footer p {
        margin: 6px 0;
        font-weight: bold;
    }

    .modal-buttons {
        display: flex;
        justify-content: space-between;
        margin-top: 200px;
    }

    .modal-buttons button {
        width: 47%;
    }

    /* Search Input Styling */
    #inventory-search {
        margin-bottom: 20px;
        padding: 12px;
        border: 1px solid #ddd;
        border-radius: 8px;
        font-size: 16px;
        width: 100%;
        box-sizing: border-box;
        transition: border-color 0.3s;
    }

    #inventory-search:focus {
        border-color: #6a0dad;
        outline: none;
    }

    /* Support Button Styling (Top-Right Corner) */
    .support-btn {
        position: absolute;
        top: 20px;
        right: 20px;
        background: #ff9800; /* Orange background for visibility */
        color: white;
        padding: 10px 15px;
        border-radius: 50px;
        cursor: pointer;
        font-size: 14px;
        font-weight: bold;
        box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
        transition: background 0.3s ease;
        z-index: 1000; /* Ensure it stays above other elements */
    }

#pos-dashboard .invoice-wrapper {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 20px;
}

#pos-dashboard .invoice-circle {
    border: 5px solid #0000FF; /* Blue border */
    border-radius: 50%; /* Makes it circular */
    padding: 30px;
    width: 500px; /* Adjust size as needed */
    height: 500px; /* Equal width and height for a perfect circle */
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #f9f9f9; /* Light background for contrast */
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); /* Optional: Add a shadow for depth */
    overflow: auto; /* Handle overflow if content exceeds the circle */
}

#pos-dashboard .invoice-circle pre {
    max-height: 100%;
    max-width: 100%;
    overflow: hidden; /* Prevent text from overflowing the circle */
}




    .support-btn:hover {
        background: #e68a00; /* Darker orange on hover */
    }

    /* Support Modal Styling */
    #support-modal {
        display: none;
        position: fixed;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        background: #fff;
        padding: 20px;
        border-radius: 10px;
        box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
        z-index: 1001; /* Above other modals */
        width: 350px;
        text-align: center;
    }

    #support-modal.active {
        display: block;
    }

    #support-modal h3 {
        color: #4b0082;
        margin-bottom: 15px;
    }




     #clear-confirmation-modal {
    width: 350px;
    text-align: center;
}

#clear-confirmation-modal p {
    color: #d32f2f;
    font-size: 14px;
    margin-bottom: 20px;
}

#clear-confirmation-modal .modal-buttons button {
    width: 48%;
}

/* Responsive adjustments for smaller screens */
@media only screen and (max-width: 600px) {
    #clear-confirmation-modal {
        width: 90%;
    }

    #clear-confirmation-modal p {
        font-size: 12px;
    }

    #clear-confirmation-modal .modal-buttons button {
        width: 100%;
        margin: 5px 0;
    }
}



    #support-modal p {
        color: #4b0082;
        font-size: 16px;
        margin-bottom: 20px;
    }

    #support-modal a {
        color: blue;
        text-decoration: underline;
        font-size: 16px;
    }
 /* AI Support Button Styling (Top-Right Corner, below Feedback) */
.ai-support-btn {
    position: absolute;
    top: 20px;
    right: 200px; /* Positioned to the left of Feedback button */
    background: #4CAF50; /* Green background for visibility */
    color: white;
    padding: 10px 15px;
    border-radius: 50px;
    cursor: pointer;
    font-size: 14px;
    font-weight: bold;
    box-shadow: 0 3px 5px rgba(0, 0, 0, 0.2);
    transition: background 0.3s ease;
    z-index: 1000;
}

.ai-support-btn:hover {
    background: #45a049; /* Darker green on hover */
}

/* AI Support Modal Styling */
/* AI Support Modal Styling */
#ai-support-modal {
    width: 600px !important;
    max-height: 80vh !important;
    display: none;
    text-align: left;
    border: 2px solid #ff0000; /* Temporary red border to confirm modal size */
}

#ai-support-modal .chat-container {
    max-height: 400px !important;
    overflow-y: auto;
    border: 1px solid #ddd;
    border-radius: 8px;
    padding: 15px;
    margin-bottom: 20px;
    background: #f9f9f9;
}

#ai-support-modal .chat-message {
    margin: 8px 0;
    padding: 10px;
    border-radius: 5px;
    font-size: 15px;
}

#ai-support-modal .bot-message {
    background: #e1f5fe;
    color: #0277bd;
    align-self: flex-start;
}

#ai-support-modal .user-message {
    background: #ede7f6;
    color: #4b0082;
    align-self: flex-end;
    margin-left: 20%;
    margin-right: 5px;
}


#ai-support-modal .chat-input #chat-input {
    flex: 1;
    padding: 14px 20px !important;
    border: 1px solid #ddd;
    border-radius: 8px;
    font-size: 16px !important;
    height: 50px !important;
    box-sizing: border-box;
    background: #ffffff; /* White background to ensure visibility */
    border: 2px solid #00ff00; /* Temporary green border to confirm input size */
}

#ai-support-modal .chat-input #chat-input:focus {
    border-color: #6a0dad;
    outline: none;
}

#ai-support-modal .chat-input button {
    padding: 14px 20px;
    height: 50px;
    font-size: 16px;
    border-radius: 8px;
}

/* Responsive adjustments for smaller screens */
@media only screen and (max-width: 600px) {
    .ai-support-btn {
        top: 10px;
        right: 10px;
        padding: 8px 12px;
        font-size: 12px;
    }

    #ai-support-modal {
        width: 90% !important;
        max-height: 70vh !important;
    }

    #ai-support-modal .chat-container {
        max-height: 300px !important;
    }

    #ai-support-modal .chat-message {
        font-size: 13px;
    }

    #ai-support-modal .chat-input {
        gap: 10px;
    }


    #ai-support-modal .chat-input button {
        padding: 10px 15px;
        font-size: 14px;
        height: 40px;
    }
}
/* Responsive adjustments for smaller screens */
@media only screen and (max-width: 600px) {
    .ai-support-btn {
        top: 10px;
        right: 10px;
        padding: 8px 12px;
        font-size: 12px;
    }

    #ai-support-modal {
        width: 90% !important;
        max-height: 70vh !important;
    }

    #ai-support-modal .chat-container {
        max-height: 300px !important;
    }

    #ai-support-modal .chat-message {
        font-size: 13px;
    }

    #ai-support-modal .chat-input {
        gap: 10px;
    }

    #ai-support-modal .chat-input #chat-input {
        padding: 10px 15px !important;
        font-size: 14px !important;
        height: 40px !important;
    }

    #ai-support-modal .chat-input button {
        padding: 10px 15px;
        font-size: 14px;
        height: 40px;
    }
}    /* Mobile devices (Android phones, smaller screens) */
    @media only screen and (max-width: 600px) {
        .container, #pos-dashboard {
            width: 100%;
            padding: 15px;
            margin: 0;
            border-radius: 0;
        }

        #pos-dashboard h2 {
            font-size: 24px;
        }

        .dashboard-tabs {
            flex-direction: column;
            gap: 10px;
        }

        .dashboard-tabs .tab {
            width: 100%;
            text-align: center;
            padding: 10px;
        }

        .item-form {
            grid-template-columns: 1fr;
            gap: 15px;
        }

        #pos-dashboard select, #pos-dashboard input[type="text"], #pos-dashboard input[type="number"], #pos-dashboard input[type="date"] {
            font-size: 16px;
        }

        .inventory-list div, .stock-list p {
            font-size: 14px;
            flex-direction: column;
            align-items: flex-start;
        }

        .inventory-list button, .stock-list button {
            width: 100%;
            margin: 5px 0;
            font-size: 14px;
        }

        .modal, #support-modal {
            width: 90%;
            max-height: 70vh;
            padding: 15px;
        }

        .modal-buttons button {
            width: 100%;
            margin: 5px 0;
        }

        .support-btn {
            top: 10px;
            right: 10px;
            padding: 8px 12px;
            font-size: 12px;
        }
    }

    /* Tablets (Android tablets, medium screens) */
    @media only screen and (min-width: 601px) and (max-width: 1024px) {
        .container, #pos-dashboard {
            width: 90%;
            padding: 20px;
        }

        .dashboard-tabs {
            flex-wrap: wrap;
            gap: 15px;
        }

        .item-form {
            grid-template-columns: repeat(2, 1fr);
        }

        .modal, #support-modal {
            width: 80%;
        }

        .support-btn {
            top: 15px;
            right: 15px;
        }
    }

    /* Desktops (Windows, larger screens) */
    @media only screen and (min-width: 1025px) {
        .container, #pos-dashboard {
            width: 80%;
            max-width: 1200px;
            margin: 0 auto;
        }

        .dashboard-tabs {
            gap: 20px;
        }

        .item-form {
            grid-template-columns: repeat(4, 1fr);
        }

        .modal, #support-modal {
            width: 600px;
        }
    }

    /* Android-specific adjustments */
    .platform-android .container,
    .platform-android #pos-dashboard {
        padding: 10px;
    }

    .platform-android button {
        font-size: 14px;
    }

    /* Windows-specific adjustments */
    .platform-windows .container,
    .platform-windows #pos-dashboard {
        padding: 30px;
    }

    .platform-windows button {
        font-size: 16px;
    }

    /* Print styles optimized for 80mm thermal printer */
    @media print {
        body {
            background: none;
            margin: 0;
            visibility: visible;
        }

        #auth-container, #pos-dashboard, #invoice-modal, #support-modal {
            display: none !important;
        }

        #printable-invoice {
            visibility: visible !important;
            display: block !important;
            position: static !important;
            transform: none !important;
            width: 80mm !important; /* Matches Shreyans thermal printer width */
            max-width: 80mm !important;
            height: auto !important;
            padding: 5mm !important;
            box-shadow: none;
            border: none;
            margin: 0;
            top: 0 !important;
            left: 0 !important;
            opacity: 1 !important;
            font-size: 10pt !important;
            line-height: 1.2 !important;
        }

        #printable-invoice * {
            visibility: visible !important;
            display: block !important;
            color: #000 !important;
        }

        #printable-invoice .modal-buttons {
            display: none !important;
        }

        #printable-invoice .invoice-table {
            font-size: 8pt !important;
            width: 100% !important;
            border-collapse: collapse;
        }

        #printable-invoice .invoice-table th,
        #printable-invoice .invoice-table td {
            border: 1px solid #000;
            padding: 2mm 1mm !important;
            text-align: left;
            word-wrap: break-word;
        }

        #printable-invoice .invoice-table th {
            background-color: #f0f0f0;
            color: #000;
        }

        #printable-invoice .invoice-table td:nth-child(2),
        #printable-invoice .invoice-table td:nth-child(3),
        #printable-invoice .invoice-table td:nth-child(4),
        #printable-invoice .invoice-table td:nth-child(5),
        #printable-invoice .invoice-table td:nth-child(6) {
            text-align: right !important;
        }

        #printable-invoice .invoice-header,
        #printable-invoice .invoice-footer {
            border-color: #000;
            font-size: 10pt !important;
        }

        #printable-invoice .invoice-details,
        #printable-invoice .invoice-table,
        #printable-invoice .invoice-footer {
            page-break-inside: avoid;
        }
    }
    </style>
</head>
<body>
    <div class="container" id="auth-container">
        <h1>KiranaKart POS</h1>
        <div class="tabs">
            <div class="tab" onclick="showTab('signup')">Sign Up</div>
            <div class="tab active" onclick="showTab('login')">Login</div>
        </div>
        <div id="signup" class="form-section" style="display: none;">
            <div class="form-group">
                <label>Store Name</label>
                <input type="text" id="signup-name" placeholder="Enter Store Name">
            </div>
            <div class="form-group">
                <label>Email</label>
                <input type="email" id="signup-email" placeholder="Enter your email">
            </div>
            <div class="form-group">
                <label>Password</label>
                <input type="password" id="signup-password" placeholder="Create a password">
            </div>
            <button onclick="signup()">Sign Up</button>
        </div>
        <div id="login" class="form-section">
            <div class="form-group">
                <label>Email</label>
                <input type="email" id="login-email" placeholder="Enter your email">
            </div>
            <div class="form-group">
                <label>Password</label>
                <input type="password" id="login-password" placeholder="Enter your password">
            </div>
            <button onclick="login()">Login</button>
        </div>
        <div id="error" class="error">Please fill in all fields correctly.</div>
    </div>

    <div class="container" id="pos-dashboard">
        <h2>KiranaKart POS Dashboard</h2>
        <p id="welcome-message" style="color: #4b0082; font-size: 16px;"></p>
        <div class="support-btn" onclick="showSupportModal()">Support</div>
        <div class="feedback-btn" onclick="showFeedbackModal()">Feedback</div>
        <div class="dashboard-tabs">
            <div class="tab active" onclick="showDashboardTab('inventory')">Inventory</div>
            <div class="tab" onclick="showDashboardTab('stock-management')">Stock Management</div>
            <div class="tab" onclick="showDashboardTab('billing')">Billing</div>
            <div class="tab" onclick="showDashboardTab('reports')">Reports</div>
            <div class="tab" onclick="showDashboardTab('suppliers')">Suppliers</div>
            <div class="tab" onclick="showDashboardTab('low-stock')">Low Stock</div>
            <div class="tab" onclick="logout()">Logout</div>
        </div>

        <div id="inventory" class="dashboard-section active">
            <h3>Manage Inventory</h3>
            <div class="form-group">
                <label for="inventory-search">Search Inventory</label>
                <input type="text" id="inventory-search" placeholder="Search by name, batch, or supplier..." oninput="searchInventory()">
            </div>
            <div class="item-form">
                <select id="item-type" onchange="toggleItemFields()">
                    <option value="loose">Loose Item</option>
                    <option value="packet">Packet Item</option>
                </select>
                <input type="text" id="item-name" placeholder="Item name">
                <input type="number" id="item-weight" placeholder="Weight (kg)" step="0.01" style="display:none;">
                <input type="number" id="item-quantity" placeholder="Quantity" step="1" style="display:none;">
                <input type="number" id="item-price" placeholder="Price per unit/kg (₹)" step="0.01">
                <input type="number" id="item-mrp" placeholder="MRP per unit/kg (₹, optional)" step="0.01">
                <input type="text" id="batch-number" placeholder="Batch No. (optional)">
                <input type="date" id="expiry-date" placeholder="Expiry Date (optional)">
                <input type="text" id="supplier" placeholder="Supplier (optional)">
                <button onclick="addItem()">Add to Inventory</button>
            </div>
            <div class="inventory-list" id="inventory-list"></div>
            <div id="quantity-modal" class="quantity-modal">
                <h3>Add to Cart with Quantity</h3>
                <div class="form-group">
                    <label>Price per Kg/Unit (₹)</label>
                    <input type="number" id="modal-price-per-kg" readonly>
                </div>
                <div class="form-group">
                    <label>Enter Amount (₹)</label>
                    <input type="number" id="modal-amount" placeholder="Enter amount" step="0.01" oninput="calculateQuantity()">
                </div>
                <div class="form-group">
                    <label>Enter Quantity</label>
                    <input type="number" id="modal-quantity" placeholder="Enter quantity" step="0.001" oninput="calculateAmount()">
                    <select id="modal-unit" onchange="updateQuantityDisplay()">
                        <option value="kg">Kilograms</option>
                        <option value="g">Grams</option>
                        <option value="units">Units</option>
                    </select>
                </div>
                <button onclick="confirmAddToCart()">Add to Cart</button>
                <button onclick="hideQuantityModal()">Cancel</button>
            </div>
            <div id="edit-modal" class="modal">
                <h3>Edit Inventory Item</h3>
                <div class="form-group">
                    <label>Item Type</label>
                    <select id="edit-item-type">
                        <option value="loose">Loose Item</option>
                        <option value="packet">Packet Item</option>
                    </select>
                </div>
                <div class="form-group">
                    <label>Item Name</label>
                    <input type="text" id="edit-item-name" placeholder="Item name">
                </div>
                <div class="form-group">
                    <label>Weight (kg)</label>
                    <input type="number" id="edit-item-weight" placeholder="Weight (kg)" step="0.01">
                </div>
                <div class="form-group">
                    <label>Quantity</label>
                    <input type="number" id="edit-item-quantity" placeholder="Quantity" step="1">
                </div>
                <div class="form-group">
                    <label>Price per unit/kg (₹)</label>
                    <input type="number" id="edit-item-price" placeholder="Price per unit/kg (₹)" step="0.01">
                </div>
                <div class="form-group">
                    <label>MRP per unit/kg (₹, optional)</label>
                    <input type="number" id="edit-item-mrp" placeholder="MRP per unit/kg (₹, optional)" step="0.01">
                </div>
                <div class="form-group">
                    <label>Batch No. (optional)</label>
                    <input type="text" id="edit-batch-number" placeholder="Batch No. (optional)">
                </div>
                <div class="form-group">
                    <label>Expiry Date (optional)</label>
                    <input type="date" id="edit-expiry-date" placeholder="Expiry Date (optional)">
                </div>
                <div class="form-group">
                    <label>Supplier (optional)</label>
                    <input type="text" id="edit-supplier" placeholder="Supplier (optional)">
                </div>
                <button onclick="saveEditedItem()">Save Changes</button>
                <button onclick="hideEditModal()">Cancel</button>
            </div>
        </div>

        <div id="stock-management" class="dashboard-section">
            <h3>Stock Management</h3>
            <div class="stock-list" id="stock-list"></div>
            <div id="stock-modal" class="stock-modal">
                <h3>Adjust Stock</h3>
                <div class="form-group">
                    <label>Item Name</label>
                    <input type="text" id="stock-item-name" readonly>
                </div>
                <div class="form-group">
                    <label>New Stock</label>
                    <input type="number" id="stock-new-value" placeholder="Enter new stock" step="0.01">
                    <select id="stock-unit">
                        <option value="kg">Kilograms</option>
                        <option value="units">Units</option>
                    </select>
                </div>
                <button onclick="adjustStock()">Save Changes</button>
                <button onclick="hideStockModal()">Cancel</button>
            </div>
        </div>

        <div id="billing" class="dashboard-section">
            <h3>Billing</h3>
            <div class="item-list" id="item-list"></div>
            <p>Total: ₹<span id="total" style="color: #4b0082; font-weight: bold;">0.00</span></p>
<button onclick="console.log('Generate Invoice button clicked'); generateInvoice()">Generate Invoice</button>        </div>

        <div id="reports" class="dashboard-section">
            <h3>Reports</h3>
            <button onclick="showReport()">View Sales Report</button>
            <button onclick="viewTransactions()">View Transactions</button>
        </div>

        <div id="suppliers" class="dashboard-section">
            <h3>Suppliers</h3>
            <button onclick="manageSuppliers()">Manage Suppliers</button>
        </div>

        <div id="low-stock" class="dashboard-section">
            <h3>Low Stock (≤ 5 units/kg)</h3>
            <div class="stock-list" id="low-stock-list"></div>
        </div>

        <div id="support-modal" class="modal">
            <h3>Support</h3>
            <p>Need help? Contact us by emailing:</p>
            <a href="https://mail.google.com/mail/?view=cm&fs=1&to=kiranakartpos@gmail.com&su=Support%20Request%20-%20KiranaKart%20POS&body=Hello%2C%0D%0AI%20am%20contacting%20you%20regarding%20an%20issue%20with%20KiranaKart%20POS.%20Please%20describe%20your%20issue%20below%3A%0D%0A%0D%0A%5BDescribe%20your%20issue%20here%5D%0D%0A%0D%0AThanks%2C%0D%0A%5BYour%20Name%5D" target="_blank">kiranakartpos@gmail.com</a>
            <div class="modal-buttons">
                <button onclick="hideSupportModal()">Close</button>
            </div>
        </div>

        <div id="feedback-modal" class="modal">
            <h3>Feedback</h3>
            <p>We'd love to hear your feedback! Please email us at:</p>
            <a href="https://mail.google.com/mail/?view=cm&fs=1&to=kiranakartpos@gmail.com&su=Feedback%20-%20KiranaKart%20POS&body=Hello%2C%0D%0AI%20am%20providing%20feedback%20for%20KiranaKart%20POS.%20%0D%0A%0D%0A%5BYour%20feedback%20here%5D%0D%0A%0D%0AThanks%2C%0D%0A%5BYour%20Name%5D" target="_blank">kiranakartpos@gmail.com</a>
            <div class="modal-buttons">
                <button onclick="hideFeedbackModal()">Close</button>
            </div>
        </div>


<div class="ai-support-btn" onclick="showAISupportModal()">AI Support</div>

<div id="ai-support-modal" class="modal">
    <h3>AI Support Assistant</h3>
    <p>Ask me anything about KiranaKart POS or general queries!</p>
    <div class="chat-container" id="chat-container">
        <div class="chat-message bot-message">Hello! How can I assist you today?</div>
    </div>
    <div class="chat-input">
        <input type="text" id="chat-input" placeholder="Type your question..." onkeypress="if(event.key === 'Enter') sendMessage()" style="height: 50px; padding: 14px 20px; font-size: 16px; border-radius: 8px;">
        <button onclick="sendMessage()">Send</button>
    </div>
    <div class="modal-buttons">
        <button onclick="hideAISupportModal()">Close</button>
    </div>
</div>







        <div id="invoice-modal" class="modal">
            <div class="invoice-header">
               <h3>Satguru Kirana Store - Invoice</h3> <!-- Add this line -->
        <p id="invoice-store">Store: </p>   
        </div>

          
            <div class="invoice-details">
                <div>
                    <p><strong>Owner:</strong> <span id="invoice-owner"></span></p>
                    <p><strong>Date:</strong> <span id="invoice-date"></span></p>
                </div>
                <div>
                                    
            </div>
            <table class="invoice-table">
                <thead>
                    <tr>
                        <th>Item</th>
                        <th>Quantity/Weight</th>
                        <th>Price (₹)</th>
                        <th>MRP (₹)</th>
                        <th>Discount (%)</th>
                        <th>Total (₹)</th>
                    </tr>
                </thead>
                <tbody id="invoice-items"></tbody>
            </table>
            <div class="invoice-footer">
<pre>







     <p id="invoice-total"></p>

</pre>
            </div>
            <div class="modal-buttons">
                <button onclick="saveTransaction()">Save Transaction</button>
                <button onclick="printInvoice()">Print</button>
                <button onclick="hideModal()">Close</button>
            </div>
        </div>

        </div>

  
      




<div id="report-modal" class="modal">
    <h3>Sales Report</h3>
    <!-- Bar Chart for Visual Representation -->
    <div style="text-align: center; margin-bottom: 20px;">
        <canvas id="sales-chart" style="max-width: 100%; max-height: 200px;"></canvas>
    </div>
    <!-- Detailed Text Report -->
    <div id="sales-details" style="font-size: 14px; margin-bottom: 20px;">
        <h4>Sales Summary</h4>
        <p><strong>Loose Items Sold:</strong> <span id="loose-sales">0</span></p>
        <p><strong>Packet Items Sold:</strong> <span id="packet-sales">0</span></p>
        <p><strong>Total Sales:</strong> ₹<span id="total-sales">0.00</span></p>
        <p><strong>Total Transactions:</strong> <span id="total-transactions">0</span></p>
        <p><strong>Average Transaction Value:</strong> ₹<span id="avg-transaction">0.00</span></p>
        <h4>Top Selling Items</h4>
        <ul id="top-items" style="list-style: none; padding: 0;"></ul>
        <h4>Sales by Item</h4>
        <div id="sales-by-item"></div>
        <h4>Sales Trend (Last 7 Days)</h4>
        <div id="sales-trend"></div>
    </div>
    <div class="modal-buttons">
        <button onclick="showClearConfirmation()" style="background: #d32f2f;">Clear Reports</button>
        <button onclick="hideModal()">Close</button>
    </div>
</div>

<!-- Confirmation Modal for Clearing Reports -->
<div id="clear-confirmation-modal" class="modal">
    <h3>Confirm Clear Reports</h3>
    <p>Are you sure you want to clear all sales reports? This action cannot be undone.</p>
    <div class="modal-buttons">
        <button onclick="clearReports()" style="background: #d32f2f;">Yes, Clear</button>
        <button onclick="hideClearConfirmation()">Cancel</button>
    </div>
</div>






        <div id="supplier-modal" class="modal">
            <h3>Supplier Management</h3>
            <input type="text" id="new-supplier" placeholder="Add new supplier">
            <button onclick="addSupplier()">Add</button>
            <ul id="supplier-list"></ul>
            <button onclick="hideModal()">Close</button>
        </div>
    </div>

    <script>
    // State variables
    let users = JSON.parse(localStorage.getItem('users')) || [];
    let inventory = JSON.parse(localStorage.getItem('inventory')) || [];
    let cart = JSON.parse(localStorage.getItem('cart')) || [];
    let suppliers = JSON.parse(localStorage.getItem('suppliers')) || [];
    let transactions = JSON.parse(localStorage.getItem('transactions')) || [];
    let offlineQueue = JSON.parse(localStorage.getItem('offlineQueue')) || [];
    let alertedItems = new Set();
    let selectedItemIndex = -1;
    let currentUser = null;


adView = new AdView(this);
adView.setAdSize(AdSize.SMART_BANNER);
adView.setAdUnitId("YOUR_AD_UNIT_ID");
adView.loadAd(new AdRequest.Builder().build());

layout.addView(webView);
layout.addView(adView);
adParams.setMargins(0, 20, 0, 0); // 20px margin above the ad






    // Initialize on page load
    document.addEventListener('DOMContentLoaded', () => {
        const lastLoggedInEmail = localStorage.getItem('lastLoggedInEmail');
        if (lastLoggedInEmail) {
            const user = users.find(u => u.email === lastLoggedInEmail);
            if (user) {
                currentUser = user;
                document.getElementById('auth-container').style.display = 'none';
                document.getElementById('pos-dashboard').style.display = 'block';
                document.getElementById('welcome-message').textContent = `Hello, ${user.name}! Manage your store.`;
            } else {
                localStorage.removeItem('lastLoggedInEmail');
                document.getElementById('auth-container').style.display = 'block';
                document.getElementById('pos-dashboard').style.display = 'none';
            }
        } else {
            document.getElementById('auth-container').style.display = 'block';
            document.getElementById('pos-dashboard').style.display = 'none';
        }

        document.getElementById('inventory-search').value = '';
        toggleItemFields();
        updateInventoryList();
        updateCart();
        updateStockList();
        updateLowStockList();
        inventory.forEach(item => checkStockAlert(item, true));
    });

    function showTab(tab) {
        document.getElementById('signup').style.display = tab === 'signup' ? 'block' : 'none';
        document.getElementById('login').style.display = tab === 'login' ? 'block' : 'none';
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        event.target.classList.add('active');
    }

function showClearConfirmation() {
    document.getElementById('clear-confirmation-modal').classList.add('active');
}

    function showDashboardTab(tab) {
        document.querySelectorAll('.dashboard-section').forEach(section => section.classList.remove('active'));
        document.querySelectorAll('.dashboard-tabs .tab').forEach(t => t.classList.remove('active'));
        document.getElementById(tab).classList.add('active');
        event.target.classList.add('active');
        if (tab === 'inventory') {
            document.getElementById('inventory-search').value = '';
            updateInventoryList();
        }
    }

    function showError(message) {
        const error = document.getElementById('error');
        error.textContent = message;
        error.classList.add('active');
        setTimeout(() => error.classList.remove('active'), 3000);
    }

    function checkStockAlert(item, forceAlert = false) {
        if (!item || typeof item !== 'object' || !item.name || !item.type) {
            console.error('Invalid item passed to checkStockAlert:', item);
            return;
        }

        const remaining = item.type === 'loose' ? item.remainingWeight : item.remainingQuantity;
        const unit = item.type === 'loose' ? 'kg' : 'units';
        const itemKey = `${item.name}-${item.type}-${item.batch || 'N/A'}-${item.expiry || 'N/A'}-${item.supplier || 'N/A'}`;

        if (isNaN(remaining) || remaining < 0) {
            console.warn(`Invalid stock value for ${item.name}: ${remaining}${unit}`);
            return;
        }

        if (remaining <= 5) {
            if (forceAlert || !alertedItems.has(itemKey)) {
                showError(`Low Stock Alert: ${item.name} has only ${remaining.toFixed(2)}${unit} remaining!`);
                alertedItems.add(itemKey);
            }
        } else {
            if (alertedItems.has(itemKey)) {
                alertedItems.delete(itemKey);
            }
        }

        updateLowStockList();
    }

    function validateEmail(email) {
        const re = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
        return re.test(email);
    }

    function signup() {
        const name = document.getElementById('signup-name').value.trim();
        const email = document.getElementById('signup-email').value.trim();
        const password = document.getElementById('signup-password').value.trim();

        if (!name || !email || !password) {
            showError("Please fill in all fields.");
            return;
        }

        if (!validateEmail(email)) {
            showError("Please enter a valid email.");
            return;
        }

        if (users.some(u => u.email === email)) {
            showError("Email already registered.");
            return;
        }

        users.push({ name, email, password });
        localStorage.setItem('users', JSON.stringify(users));
        showError("Sign up successful! Please log in.");
        document.getElementById('signup-name').value = '';
        document.getElementById('signup-email').value = '';
        document.getElementById('signup-password').value = '';
    }










    function login() {
    const email = document.getElementById('login-email').value.trim();
    const password = document.getElementById('login-password').value.trim();

    if (!email || !password) {
        showError("Please fill in all fields.");
        return;
    }

    if (!validateEmail(email)) {
        showError("Please enter a valid email.");
        return;
    }

    const user = users.find(u => u.email === email && u.password === password);
    if (!user) {
        showError("Invalid email or password.");
        return;
    }

    currentUser = user; // Set currentUser
            localStorage.setItem('lastLoggedInEmail', email);
    // showSuccess("Login successful!"); // showSuccess is not defined, replace with showError
            showError("Login successful!");
            document.getElementById('auth-container').style.display = 'none';
           document.getElementById('pos-dashboard').style.display = 'block'; // Fix: Use pos-dashboard instead of main-container
          showDashboardTab('inventory'); // Fix: Use showDashboardTab instead of showTab
             document.getElementById('welcome-message').textContent = `Hello, ${user.name}! Manage your store.`; // Ensure welcome   message is set
}










    function logout() {
        currentUser = null;
        localStorage.removeItem('lastLoggedInEmail');
        document.getElementById('pos-dashboard').style.display = 'none';
        document.getElementById('auth-container').style.display = 'block';
        document.getElementById('login-email').value = '';
        document.getElementById('login-password').value = '';
    }

    function toggleItemFields() {
        const type = document.getElementById('item-type').value;
        const weightField = document.getElementById('item-weight');
        const quantityField = document.getElementById('item-quantity');

        weightField.style.display = type === 'loose' ? 'block' : 'none';
        quantityField.style.display = type === 'packet' ? 'block' : 'none';

        if (type === 'loose') {
            quantityField.value = '';
        } else {
            weightField.value = '';
        }
    }

    function addItem() {
        try {
            const type = document.getElementById('item-type').value;
            const name = document.getElementById('item-name').value.trim();
            const weight = type === 'loose' ? parseFloat(document.getElementById('item-weight').value) || 0 : 0;
            const quantity = type === 'packet' ? parseInt(document.getElementById('item-quantity').value) || 0 : 0;
            const price = parseFloat(document.getElementById('item-price').value) || 0;
            const mrp = parseFloat(document.getElementById('item-mrp').value) || 0;
            const batch = document.getElementById('batch-number').value.trim() || 'N/A';
            const expiry = document.getElementById('expiry-date').value || 'N/A';
            const supplier = document.getElementById('supplier').value.trim() || 'N/A';

            if (!name) {
                showError("Item name is required.");
                return;
            }
            if (isNaN(price) || price <= 0) {
                showError("Price must be a valid number greater than 0.");
                return;
            }
            if (type === 'loose' && (isNaN(weight) || weight <= 0)) {
                showError("Weight must be a valid number greater than 0 for loose items.");
                return;
            }
            if (type === 'packet' && (isNaN(quantity) || quantity <= 0)) {
                showError("Quantity must be a valid number greater than 0 for packet items.");
                return;
            }
            if (mrp > 0 && mrp < price) {
                showError("MRP cannot be less than the purchase price.");
                return;
            }

            const finalMrp = mrp > 0 ? mrp : price * 1.10;
            const item = { type, name, weight, quantity, remainingWeight: weight, remainingQuantity: quantity, price, mrp: finalMrp, batch, expiry, supplier };
            inventory.push(item);
            localStorage.setItem('inventory', JSON.stringify(inventory));
            updateInventoryList();
            updateStockList();
            checkStockAlert(item);

            document.getElementById('inventory-search').value = '';
            document.getElementById('item-name').value = '';
            document.getElementById('item-weight').value = '';
            document.getElementById('item-quantity').value = '';
            document.getElementById('item-price').value = '';
            document.getElementById('item-mrp').value = '';
            document.getElementById('batch-number').value = '';
            document.getElementById('expiry-date').value = '';
            document.getElementById('supplier').value = '';
            showError("Item added successfully!");
        } catch (error) {
            console.error('Error adding item:', error);
            showError("Failed to add item.");
        }
    }

    function searchInventory() {
        const searchTerm = document.getElementById('inventory-search').value.trim().toLowerCase();
        const filteredInventory = inventory.filter(item => {
            return (
                item.name.toLowerCase().includes(searchTerm) ||
                item.batch.toLowerCase().includes(searchTerm) ||
                item.supplier.toLowerCase().includes(searchTerm)
            );
        });
        updateInventoryList(filteredInventory);
    }




   function updateInventoryList(filteredInventory = inventory) {
    try {
        const inventoryList = document.getElementById('inventory-list');
        if (!inventoryList) {
            throw new Error("Inventory list element not found.");
        }

        inventoryList.innerHTML = filteredInventory.map((item, index) => {
            if (!item || !item.name || typeof item.price !== 'number') {
                console.warn('Invalid inventory item:', item);
                return '';
            }
            const mrp = item.mrp || (item.price * 1.10);
            const discount = mrp > item.price ? ((mrp - item.price) / mrp * 100).toFixed(2) : 0;
            const remaining = item.type === 'loose' ? item.remainingWeight : item.remainingQuantity;
            const originalIndex = inventory.indexOf(item);
            return `
                <div>
                    <span style="flex: 1;">
                        ${item.name} (${item.type === 'loose' ? `${item.weight.toFixed(2)}kg` : `${item.quantity} units`}, Remaining: ${remaining.toFixed(2)}${item.type === 'loose' ? 'kg' : ' units'})
                    </span>
                    <span style="text-align: right; min-width: 250px;">
                        ₹${item.price.toFixed(2)} | MRP: ₹${mrp.toFixed(2)} | Discount: ${discount}% | Batch: ${item.batch} | Expiry: ${item.expiry} | Supplier: ${item.supplier}
                    </span>
                    <div style="margin-left: 10px;">
                        <button onclick="showQuantityModal(${originalIndex})">Select Quantity</button>
                        <button onclick="addToCartFromInventory(${originalIndex})">Add to Cart</button>
                        <button onclick="removeFromInventory(${originalIndex})" style="background: #d32f2f;">Remove</button>
                        <button onclick="showEditModal(${originalIndex})" style="background: #ff9800;">Edit</button>
                    </div>
                </div>
            `;
        }).filter(item => item !== '').join('');
    } catch (error) {
        console.error('Error updating inventory list:', error);
        showError("Failed to update inventory list.");
    }
}



    function showEditModal(index) {
        selectedItemIndex = index;
        const item = inventory[index];
        document.getElementById('edit-item-type').value = item.type;
        document.getElementById('edit-item-name').value = item.name;
        document.getElementById('edit-item-weight').value = item.type === 'loose' ? item.weight : '';
        document.getElementById('edit-item-quantity').value = item.type === 'packet' ? item.quantity : '';
        document.getElementById('edit-item-price').value = item.price;
        document.getElementById('edit-item-mrp').value = item.mrp || '';
        document.getElementById('edit-batch-number').value = item.batch;
        document.getElementById('edit-expiry-date').value = item.expiry !== 'N/A' ? item.expiry : '';
        document.getElementById('edit-supplier').value = item.supplier;
        document.getElementById('edit-modal').classList.add('active');
    }

    function hideEditModal() {
        document.getElementById('edit-modal').classList.remove('active');
        selectedItemIndex = -1;
    }

    function saveEditedItem() {
        try {
            if (selectedItemIndex < 0 || selectedItemIndex >= inventory.length) {
                showError("No item selected for editing.");
                return;
            }

            const type = document.getElementById('edit-item-type').value;
            const name = document.getElementById('edit-item-name').value.trim();
            const weight = type === 'loose' ? parseFloat(document.getElementById('edit-item-weight').value) || 0 : 0;
            const quantity = type === 'packet' ? parseInt(document.getElementById('edit-item-quantity').value) || 0 : 0;
            const price = parseFloat(document.getElementById('edit-item-price').value) || 0;
            const mrp = parseFloat(document.getElementById('edit-item-mrp').value) || 0;
            const batch = document.getElementById('edit-batch-number').value.trim() || 'N/A';
            const expiry = document.getElementById('edit-expiry-date').value || 'N/A';
            const supplier = document.getElementById('edit-supplier').value.trim() || 'N/A';

            if (!name) {
                showError("Item name is required.");
                return;
            }
            if (isNaN(price) || price <= 0) {
                showError("Price must be a valid number greater than 0.");
                return;
            }
            if (type === 'loose' && (isNaN(weight) || weight <= 0)) {
                showError("Weight must be a valid number greater than 0 for loose items.");
                return;
            }
            if (type === 'packet' && (isNaN(quantity) || quantity <= 0)) {
                showError("Quantity must be a valid number greater than 0 for packet items.");
                return;
            }
            if (mrp > 0 && mrp < price) {
                showError("MRP cannot be less than the purchase price.");
                return;
            }

            const finalMrp = mrp > 0 ? mrp : price * 1.10;
            const remainingWeight = type === 'loose' ? weight : inventory[selectedItemIndex].remainingWeight;
            const remainingQuantity = type === 'packet' ? quantity : inventory[selectedItemIndex].remainingQuantity;
            inventory[selectedItemIndex] = { type, name, weight, quantity, remainingWeight, remainingQuantity, price, mrp: finalMrp, batch, expiry, supplier };
            localStorage.setItem('inventory', JSON.stringify(inventory));
            updateInventoryList();
            updateStockList();
            checkStockAlert(inventory[selectedItemIndex]);
            document.getElementById('inventory-search').value = '';
            hideEditModal();
            showError("Item updated successfully!");
        } catch (error) {
            console.error('Error editing item:', error);
            showError("Failed to update item.");
        }
    }

    function addToCartFromInventory(index) {
        try {
            if (index < 0 || index >= inventory.length) {
                throw new Error("Invalid item index.");
            }

            const selectedItem = inventory[index];
            const initialWeight = selectedItem.type === 'loose' ? selectedItem.weight : 0;
            const initialQuantity = selectedItem.type === 'packet' ? selectedItem.quantity : 0;
            const remainingWeight = selectedItem.remainingWeight || 0;
            const remainingQuantity = selectedItem.remainingQuantity || 0;

            if (selectedItem.type === 'loose' && initialWeight > remainingWeight) {
                throw new Error(`Not enough stock: ${initialWeight}kg requested, ${remainingWeight}kg available.`);
            }
            if (selectedItem.type === 'packet' && initialQuantity > remainingQuantity) {
                throw new Error(`Not enough stock: ${initialQuantity} units requested, ${remainingQuantity} units available.`);
            }

            const itemCost = selectedItem.price * (selectedItem.type === 'loose' ? initialWeight : initialQuantity);
            const mrp = selectedItem.mrp || (selectedItem.price * 1.10);
            const discountPercentage = mrp > selectedItem.price ? ((mrp - selectedItem.price) / mrp * 100).toFixed(2) : 0;
            const discountedPricePerUnit = selectedItem.price;

            const cartItem = {
                type: selectedItem.type,
                name: selectedItem.name,
                weight: initialWeight,
                quantity: initialQuantity,
                price: selectedItem.price,
                mrp: mrp,
                discount: discountPercentage,
                discountedPrice: discountedPricePerUnit,
                cost: itemCost,
                batch: selectedItem.batch,
                expiry: selectedItem.expiry,
                supplier: selectedItem.supplier
            };
            cart.push(cartItem);

            if (selectedItem.type === 'loose') {
                selectedItem.remainingWeight -= initialWeight;
            } else {
                selectedItem.remainingQuantity -= initialQuantity;
            }

            localStorage.setItem('inventory', JSON.stringify(inventory));
            localStorage.setItem('cart', JSON.stringify(cart));
            updateCart();
            updateInventoryList();
            updateStockList();
            checkStockAlert(selectedItem);
            showDashboardTab('billing');
            showError("Item added to cart!");
        } catch (error) {
            console.error('Error adding to cart:', error);
            showError(error.message);
        }
    }

    function removeFromInventory(index) {
        try {
            if (index < 0 || index >= inventory.length) {
                showError("Invalid item index.");
                return;
            }
            const item = inventory[index];
            const itemKey = `${item.name}-${item.type}-${item.batch || 'N/A'}-${item.expiry || 'N/A'}-${item.supplier || 'N/A'}`;
            inventory.splice(index, 1);
            alertedItems.delete(itemKey);
            localStorage.setItem('inventory', JSON.stringify(inventory));
            updateInventoryList();
            updateStockList();
            updateLowStockList();
            document.getElementById('inventory-search').value = '';
            showError("Item removed from inventory!");
        } catch (error) {
            console.error('Error removing item:', error);
            showError("Failed to remove item.");
        }
    }

    function removeFromCart(index) {
        try {
            if (index < 0 || index >= cart.length) {
                showError("Invalid cart item index.");
                return;
            }

            const cartItem = cart[index];
            const inventoryItem = inventory.find(item => item.name === cartItem.name && item.type === cartItem.type && item.batch === cartItem.batch && item.expiry === cartItem.expiry && item.supplier === cartItem.supplier);

            if (inventoryItem) {
                if (cartItem.type === 'loose') {
                    inventoryItem.remainingWeight += cartItem.weight;
                } else {
                    inventoryItem.remainingQuantity += cartItem.quantity;
                }
                checkStockAlert(inventoryItem);
            }

            cart.splice(index, 1);
            localStorage.setItem('cart', JSON.stringify(cart));
            localStorage.setItem('inventory', JSON.stringify(inventory));
            updateCart();
            updateInventoryList();
            updateStockList();
            updateLowStockList();
            showError("Item removed from cart!");
        } catch (error) {
            console.error('Error removing from cart:', error);
            showError("Failed to remove item from cart.");
        }
    }

    function updateCart() {
    try {
        const itemList = document.getElementById('item-list');
        if (!itemList) {
            throw new Error("Item list element not found.");
        }

        itemList.innerHTML = cart.map((item, index) => {
            if (!item || !item.name || typeof item.price !== 'number') {
                console.warn('Invalid cart item:', item);
                return '';
            }
            return `
                <div>
                    <span style="flex: 1;">
                        ${item.name} (${item.type === 'loose' ? `${item.weight.toFixed(2)}kg` : `${item.quantity} units`})
                    </span>
                    <span style="text-align: right; min-width: 200px;">
                        Price: ₹${item.price.toFixed(2)}/${item.type === 'loose' ? 'kg' : 'unit'} | 
                        MRP: ₹${item.mrp.toFixed(2)} | 
                        Discount: ${item.discount}% | 
                        Total: ₹${item.cost.toFixed(2)}
                    </span>
                    <button onclick="removeFromCart(${index})">Remove</button>
                </div>
            `;
        }).filter(item => item !== '').join('');

        const total = cart.reduce((sum, item) => sum + (item.cost || 0), 0);
        const totalElement = document.getElementById('total');
        if (totalElement) {
            totalElement.textContent = total.toFixed(2);
        }
    } catch (error) {
        console.error('Error updating cart:', error);
        showError("Failed to update cart display.");
    }
}












function generateInvoice() {
    console.log("generateInvoice called");
    console.log("Cart:", cart);
    console.log("CurrentUser:", currentUser);

    if (!currentUser || !currentUser.name) {
        console.log("Error: User not logged in");
        showError("User not logged in. Please log in to generate an invoice.");
        return;
    }

    if (cart.length === 0) {
        console.log("Error: Cart is empty");
        showError("Cart is empty. Add items to generate an invoice.");
        return;
    }

    console.log("Generating invoice...");
    const invoiceDate = new Date().toLocaleString();


    const invoiceItems = cart.map(item => `
        <tr>
            <td>${item.name}</td>
            <td>${item.type === 'loose' ? `${item.weight.toFixed(2)}kg` : `${item.quantity} units`}</td>
            <td>₹${item.price.toFixed(2)}</td>
            <td>₹${item.mrp.toFixed(2)}</td>
            <td>${item.discount}%</td>
            <td>₹${item.cost.toFixed(2)}</td>
        </tr>
    `).join('');
    const total = cart.reduce((sum, item) => sum + item.cost, 0);
    document.getElementById('invoice-owner').textContent = `Owner: ${currentUser.name}`;
    document.getElementById('invoice-date').textContent = `Date: ${invoiceDate}`;
    document.getElementById('invoice-store').textContent = `Store: ${currentUser.name}`;
    document.getElementById('invoice-items').innerHTML = invoiceItems;
    document.getElementById('invoice-total').textContent = `Total: ₹${total.toFixed(2)}`;
    document.querySelector('#invoice-modal .invoice-header h3').textContent = `${currentUser.name} - Invoice`;
    document.getElementById('invoice-modal').classList.add('active');
    console.log("Invoice generated successfully");
}








    function saveTransaction() {
        try {
            const transaction = {
                date: new Date().toLocaleString(),
                items: [...cart],
                total: cart.reduce((sum, item) => sum + item.cost, 0)
            };
            transactions.push(transaction);
            localStorage.setItem('transactions', JSON.stringify(transactions));
            cart = [];
            localStorage.setItem('cart', JSON.stringify(cart));
            updateCart();
            updateInventoryList();
            updateStockList();
            hideModal();
            showError("Transaction saved successfully!");
        } catch (error) {
            console.error('Error saving transaction:', error);
            showError("Failed to save transaction.");
        }
    }

    function viewTransactions() {
        const transactionList = document.getElementById('transaction-list');
        if (transactions.length === 0) {
            transactionList.innerHTML = '<p>No transactions found.</p>';
        } else {
            transactionList.innerHTML = transactions.map((t, index) => `
                <p><strong>Transaction ${index + 1} (${t.date})</strong></p>
                ${t.items.map(item => `<p>${item.name} (${item.type === 'loose' ? `${item.weight.toFixed(2)}kg` : `${item.quantity} units`}): ₹${item.cost.toFixed(2)}</p>`).join('')}
                <p>Total: ₹${t.total.toFixed(2)}</p>
                <hr>
            `).join('');
        }
        document.getElementById('transaction-modal').classList.add('active');
    }










   function showReport() {
    // Calculate basic sales metrics
    const looseSales = transactions.flatMap(t => t.items).filter(item => item.type === 'loose').length;
    const packetSales = transactions.flatMap(t => t.items).filter(item => item.type === 'packet').length;
    const totalSales = transactions.reduce((sum, t) => sum + t.total, 0);
    const totalTransactions = transactions.length;
    const avgTransaction = totalTransactions > 0 ? (totalSales / totalTransactions).toFixed(2) : 0.00;

    // Update basic sales summary
    document.getElementById('loose-sales').textContent = looseSales;
    document.getElementById('packet-sales').textContent = packetSales;
    document.getElementById('total-sales').textContent = totalSales.toFixed(2);
    document.getElementById('total-transactions').textContent = totalTransactions;
    document.getElementById('avg-transaction').textContent = avgTransaction;

    // Draw Bar Chart for Loose vs. Packet Sales
    const ctx = document.getElementById('sales-chart').getContext('2d');
    const chartWidth = 300;
    const chartHeight = 150;
    const barWidth = 60;
    const maxHeight = 100;
    const scale = maxHeight / Math.max(looseSales, packetSales, 1); // Avoid division by zero

    // Set canvas dimensions
    ctx.canvas.width = chartWidth;
    ctx.canvas.height = chartHeight;

    // Clear canvas
    ctx.clearRect(0, 0, chartWidth, chartHeight);

    // Draw background
    ctx.fillStyle = '#f0f0f0';
    ctx.fillRect(0, 0, chartWidth, chartHeight);

    // Draw bars
    // Loose Items Bar
    const looseHeight = looseSales * scale;
    ctx.fillStyle = '#6a0dad'; // Purple for loose items
    ctx.fillRect(80, chartHeight - looseHeight - 30, barWidth, looseHeight);
    ctx.fillStyle = '#000';
    ctx.font = '12px Arial';
    ctx.textAlign = 'center';
    ctx.fillText('Loose', 80 + barWidth / 2, chartHeight - 10);
    ctx.fillText(looseSales, 80 + barWidth / 2, chartHeight - looseHeight - 40);

    // Packet Items Bar
    const packetHeight = packetSales * scale;
    ctx.fillStyle = '#ff9800'; // Orange for packet items
    ctx.fillRect(160, chartHeight - packetHeight - 30, barWidth, packetHeight);
    ctx.fillStyle = '#000';
    ctx.font = '12px Arial';
    ctx.textAlign = 'center';
    ctx.fillText('Packet', 160 + barWidth / 2, chartHeight - 10);
    ctx.fillText(packetSales, 160 + barWidth / 2, chartHeight - packetHeight - 40);

    // Draw chart title
    ctx.fillStyle = '#4b0082';
    ctx.font = '14px Arial';
    ctx.fillText('Sales by Item Type', chartWidth / 2, 20);

    // Sales by Item Breakdown
    const allItems = transactions.flatMap(t => t.items);
    const itemSales = {};
    allItems.forEach(item => {
        const key = `${item.name} (${item.type})`;
        if (!itemSales[key]) {
            itemSales[key] = { count: 0, total: 0 };
        }
        itemSales[key].count += item.type === 'loose' ? item.weight : item.quantity;
        itemSales[key].total += item.cost;
    });

    const salesByItem = document.getElementById('sales-by-item');
    salesByItem.innerHTML = Object.entries(itemSales).map(([key, data]) => `
        <p>${key}: ${data.count.toFixed(2)} sold, ₹${data.total.toFixed(2)}</p>
    `).join('');

    // Top Selling Items (by quantity sold)
    const topItems = Object.entries(itemSales)
        .sort((a, b) => b[1].count - a[1].count)
        .slice(0, 5);
    const topItemsList = document.getElementById('top-items');
    topItemsList.innerHTML = topItems.length > 0
        ? topItems.map(([key, data]) => `<li>${key}: ${data.count.toFixed(2)} sold</li>`).join('')
        : '<li>No sales data available.</li>';

    // Sales Trend (Last 7 Days)
    const today = new Date('2025-05-16T11:49:00+05:30'); // Current date and time as per your input
    const sevenDaysAgo = new Date(today);
    sevenDaysAgo.setDate(today.getDate() - 7);

    const dailySales = {};
    for (let i = 0; i < 7; i++) {
        const date = new Date(sevenDaysAgo);
        date.setDate(sevenDaysAgo.getDate() + i);
        const dateStr = date.toLocaleDateString('en-IN', { day: '2-digit', month: '2-digit', year: 'numeric' });
        dailySales[dateStr] = 0;
    }

    transactions.forEach(t => {
        const transactionDate = new Date(t.date);
        if (transactionDate >= sevenDaysAgo && transactionDate <= today) {
            const dateStr = transactionDate.toLocaleDateString('en-IN', { day: '2-digit', month: '2-digit', year: 'numeric' });
            dailySales[dateStr] = (dailySales[dateStr] || 0) + t.total;
        }
    });

    const salesTrend = document.getElementById('sales-trend');
    salesTrend.innerHTML = Object.entries(dailySales).map(([date, total]) => `
        <p>${date}: ₹${total.toFixed(2)}</p>
    `).join('');

    // Show the modal
    document.getElementById('report-modal').classList.add('active');
}


function clearReports() {
    try {
        // Clear transactions
        transactions = [];
        localStorage.setItem('transactions', JSON.stringify(transactions));
        
        // Update the report modal to reflect cleared data
        document.getElementById('loose-sales').textContent = '0';
        document.getElementById('packet-sales').textContent = '0';
        document.getElementById('total-sales').textContent = '0.00';
        document.getElementById('total-transactions').textContent = '0';
        document.getElementById('avg-transaction').textContent = '0.00';
        document.getElementById('top-items').innerHTML = '<li>No sales data available.</li>';
        document.getElementById('sales-by-item').innerHTML = '';
        
        // Clear sales trend (last 7 days)
        const today = new Date('2025-05-16T14:43:00+05:30'); // Updated to current time
        const sevenDaysAgo = new Date(today);
        sevenDaysAgo.setDate(today.getDate() - 7);
        const dailySales = {};
        for (let i = 0; i < 7; i++) {
            const date = new Date(sevenDaysAgo);
            date.setDate(sevenDaysAgo.getDate() + i);
            const dateStr = date.toLocaleDateString('en-IN', { day: '2-digit', month: '2-digit', year: 'numeric' });
            dailySales[dateStr] = 0;
        }
        const salesTrend = document.getElementById('sales-trend');
        salesTrend.innerHTML = Object.entries(dailySales).map(([date, total]) => `
            <p>${date}: ₹${total.toFixed(2)}</p>
        `).join('');

        // Clear the chart
        const ctx = document.getElementById('sales-chart').getContext('2d');
        const chartWidth = 300;
        const chartHeight = 150;
        ctx.clearRect(0, 0, chartWidth, chartHeight);
        ctx.fillStyle = '#f0f0f0';
        ctx.fillRect(0, 0, chartWidth, chartHeight);
        ctx.fillStyle = '#4b0082';
        ctx.font = '14px Arial';
        ctx.textAlign = 'center';
        ctx.fillText('Sales by Item Type', chartWidth / 2, 20);
        ctx.fillStyle = '#6a0dad';
        ctx.fillRect(80, chartHeight - 30, 60, 0);
        ctx.fillStyle = '#ff9800';
        ctx.fillRect(160, chartHeight - 30, 60, 0);
        ctx.fillStyle = '#000';
        ctx.font = '12px Arial';
        ctx.fillText('Loose', 110, chartHeight - 10);
        ctx.fillText('0', 110, chartHeight - 40);
        ctx.fillText('Packet', 190, chartHeight - 10);
        ctx.fillText('0', 190, chartHeight - 40);

        // Hide the confirmation modal
        hideClearConfirmation();
        showError("Reports cleared successfully!");
    } catch (error) {
        console.error('Error clearing reports:', error);
        showError("Failed to clear reports.");
    }
}
function hideClearConfirmation() {
    document.getElementById('clear-confirmation-modal').classList.remove('active');
}












    function manageSuppliers() {
        document.getElementById('supplier-list').innerHTML = suppliers.map(s => `<li>${s}</li>`).join('');
        document.getElementById('supplier-modal').classList.add('active');
    }

    function addSupplier() {
        const supplier = document.getElementById('new-supplier').value.trim();
        if (supplier && !suppliers.includes(supplier)) {
            suppliers.push(supplier);
            localStorage.setItem('suppliers', JSON.stringify(suppliers));
            document.getElementById('new-supplier').value = '';
            manageSuppliers();
            showError("Supplier added successfully!");
        } else {
            showError("Supplier name is invalid or already exists.");
        }
    }

    function hideModal() {
        document.querySelectorAll('.modal').forEach(modal => {
            modal.classList.remove('active');
            modal.style.display = '';
        });
    }

    function showQuantityModal(index) {
        selectedItemIndex = index;
        const item = inventory[index];
        document.getElementById('modal-price-per-kg').value = item.price.toFixed(2);
        document.getElementById('modal-amount').value = '';
        document.getElementById('modal-quantity').value = '';
        document.getElementById('modal-unit').value = item.type === 'loose' ? 'kg' : 'units';
        document.getElementById('quantity-modal').classList.add('active');
    }

    function hideQuantityModal() {
        document.getElementById('quantity-modal').classList.remove('active');
        selectedItemIndex = -1;
    }

    function calculateQuantity() {
        const pricePerUnit = parseFloat(document.getElementById('modal-price-per-kg').value);
        const amount = parseFloat(document.getElementById('modal-amount').value);
        if (isNaN(pricePerUnit) || isNaN(amount) || pricePerUnit <= 0) {
            document.getElementById('modal-quantity').value = '';
            return;
        }
        let quantity = amount / pricePerUnit;
        const unit = document.getElementById('modal-unit').value;
        if (unit === 'g') {
            quantity *= 1000;
        }
        document.getElementById('modal-quantity').value = quantity.toFixed(3);
    }

    function calculateAmount() {
        const pricePerUnit = parseFloat(document.getElementById('modal-price-per-kg').value);
        let quantity = parseFloat(document.getElementById('modal-quantity').value);
        const unit = document.getElementById('modal-unit').value;
        if (isNaN(pricePerUnit) || isNaN(quantity) || pricePerUnit <= 0 || quantity <= 0) {
            document.getElementById('modal-amount').value = '';
            return;
        }
        if (unit === 'g') {
            quantity /= 1000;
        }
        const amount = quantity * pricePerUnit;
        document.getElementById('modal-amount').value = amount.toFixed(2);
    }

    function updateQuantityDisplay() {
        const quantity = parseFloat(document.getElementById('modal-quantity').value);
        if (isNaN(quantity)) return;
        const unit = document.getElementById('modal-unit').value;
        if (unit === 'g') {
            document.getElementById('modal-quantity').value = (quantity * 1000).toFixed(3);
        } else {
            document.getElementById('modal-quantity').value = (quantity / 1000).toFixed(3);
        }
        calculateAmount();
    }

    function confirmAddToCart() {
        try {
            if (selectedItemIndex < 0 || selectedItemIndex >= inventory.length) {
                showError("Invalid item selected.");
                return;
            }

            const item = inventory[selectedItemIndex];
            let quantity = parseFloat(document.getElementById('modal-quantity').value);
            const unit = document.getElementById('modal-unit').value;

            if (isNaN(quantity) || quantity <= 0) {
                showError("Enter a valid quantity.");
                return;
            }

            if (unit === 'g') {
                quantity /= 1000;
            }

            if (item.type === 'loose' && quantity > item.remainingWeight) {
                showError(`Not enough stock: ${quantity.toFixed(2)}kg requested, ${item.remainingWeight.toFixed(2)}kg available.`);
                return;
            }
            if (item.type === 'packet' && quantity > item.remainingQuantity) {
                showError(`Not enough stock: ${quantity} units requested, ${item.remainingQuantity} units available.`);
                return;
            }

            const itemCost = item.price * quantity;
            const mrp = item.mrp || (item.price * 1.10);
            const discountPercentage = mrp > item.price ? ((mrp - item.price) / mrp * 100).toFixed(2) : 0;
            const cartItem = {
                type: item.type,
                name: item.name,
                weight: item.type === 'loose' ? quantity : 0,
                quantity: item.type === 'packet' ? quantity : 0,
                price: item.price,
                mrp: mrp,
                discount: discountPercentage,
                cost: itemCost,
                batch: item.batch,
                expiry: item.expiry,
                supplier: item.supplier
            };
            cart.push(cartItem);

            if (item.type === 'loose') {
                item.remainingWeight -= quantity;
            } else {
                item.remainingQuantity -= quantity;
            }

            localStorage.setItem('inventory', JSON.stringify(inventory));
            localStorage.setItem('cart', JSON.stringify(cart));
            updateCart();
            updateInventoryList();
            updateStockList();
            checkStockAlert(item);
            hideQuantityModal();
            showError("Item added to cart!");
        } catch (error) {
            console.error('Error adding to cart:', error);
            showError("Failed to add item to cart.");
        }
    }

    function printInvoice() {
        const invoiceModal = document.getElementById('invoice-modal');
        if (!invoiceModal.classList.contains('active')) {
            generateInvoice();
        }

        const printContent = document.createElement('div');
        printContent.innerHTML = invoiceModal.innerHTML;
        printContent.id = 'printable-invoice';
        printContent.style.visibility = 'visible';
        printContent.style.display = 'block';
        printContent.style.position = 'static';
        printContent.style.width = '80mm';
        printContent.style.padding = '5mm';
        document.body.appendChild(printContent);

        const wasActive = invoiceModal.classList.contains('active');
        invoiceModal.classList.remove('active');
        document.body.style.visibility = 'hidden';
        document.getElementById('auth-container').style.display = 'none';
        document.getElementById('pos-dashboard').style.display = 'none';

        window.print();

        window.onafterprint = () => {
            document.body.removeChild(printContent);
            document.body.style.visibility = 'visible';
            if (currentUser) {
                document.getElementById('pos-dashboard').style.display = 'block';
                document.getElementById('auth-container').style.display = 'none';
            } else {
                document.getElementById('pos-dashboard').style.display = 'none';
                document.getElementById('auth-container').style.display = 'block';
            }
            if (wasActive) {
                invoiceModal.classList.add('active');
            }
            invoiceModal.style.display = '';
            window.onafterprint = null;
        };
    }

    function syncOffline() {
        if (navigator.onLine) {
            offlineQueue.forEach(item => cart.push(item));
            localStorage.setItem('cart', JSON.stringify(cart));
            offlineQueue = [];
            localStorage.setItem('offlineQueue', JSON.stringify(offlineQueue));
            updateCart();
        }
    }
    window.addEventListener('online', syncOffline);

    function updateStockList() {
    try {
        const stockList = document.getElementById('stock-list');
        if (!stockList) {
            throw new Error("Stock list element not found.");
        }

        stockList.innerHTML = inventory.map((item, index) => {
            if (!item || !item.name) {
                console.warn('Invalid stock item:', item);
                return '';
            }
            const remaining = item.type === 'loose' ? item.remainingWeight : item.remainingQuantity;
            return `
                <p>
                    ${item.name} (Remaining: ${remaining.toFixed(2)}${item.type === 'loose' ? 'kg' : ' units'})
                    <button onclick="showStockModal(${index}, 'add')">Add Stock</button>
                    <button onclick="showStockModal(${index}, 'edit')">Edit Stock</button>
                </p>
            `;
        }).filter(item => item !== '').join('');
    } catch (error) {
        console.error('Error updating stock list:', error);
        showError("Failed to update stock list.");
    }
}

    function showStockModal(index, action) {
        selectedItemIndex = index;
        const item = inventory[index];
        if (!item) {
            showError("Invalid item selected.");
            return;
        }
        document.getElementById('stock-item-name').value = item.name;
        document.getElementById('stock-new-value').value = item.type === 'loose' ? item.remainingWeight.toFixed(2) : item.remainingQuantity.toFixed(2);
        document.getElementById('stock-unit').value = item.type === 'loose' ? 'kg' : 'units';
        document.getElementById('stock-modal').classList.add('active');
    }

    function hideStockModal() {
        document.getElementById('stock-modal').classList.remove('active');
        selectedItemIndex = -1;
    }

    function adjustStock() {
        try {
            if (selectedItemIndex < 0 || selectedItemIndex >= inventory.length) {
                showError("Invalid item selected.");
                return;
            }

            const item = inventory[selectedItemIndex];
            const newValue = parseFloat(document.getElementById('stock-new-value').value);
            const unit = document.getElementById('stock-unit').value;

            if (isNaN(newValue) || newValue < 0) {
                showError("Please enter a valid positive stock value.");
                return;
            }

            if (unit === 'kg' && item.type !== 'loose') {
                showError("Cannot set kilograms for packet items.");
                return;
            }
            if (unit === 'units' && item.type !== 'packet') {
                showError("Cannot set units for loose items.");
                return;
            }

            const previousRemaining = item.type === 'loose' ? item.remainingWeight : item.remainingQuantity;
            if (unit === 'kg') {
                item.remainingWeight = newValue;
            } else {
                item.remainingQuantity = newValue;
            }

            if (newValue < (item.type === 'loose' ? item.weight : item.quantity)) {
                if (item.type === 'loose') {
                    item.weight = newValue;
                } else {
                    item.quantity = newValue;
                }
            }

            localStorage.setItem('inventory', JSON.stringify(inventory));
            updateInventoryList();
            updateStockList();
            updateLowStockList();
            checkStockAlert(item);

            const newRemaining = item.type === 'loose' ? item.remainingWeight : item.remainingQuantity;
            if (newRemaining > 5 && previousRemaining <= 5) {
                showError("Stock adjusted successfully! Low stock alert cleared.");
            } else if (newRemaining <= 5 && previousRemaining > 5) {
                showError("Stock adjusted successfully! Low stock alert triggered.");
            } else {
                showError("Stock adjusted successfully!");
            }

            hideStockModal();
        } catch (error) {
            console.error('Error adjusting stock:', error);
            showError("Failed to adjust stock. Please try again.");
        }
    }

    function updateLowStockList() {
        const lowStockList = document.getElementById('low-stock-list');
        if (!lowStockList) {
            console.error('Low stock list element not found.');
            return;
        }
        const lowStockItems = inventory.filter(item => {
            const remaining = item.type === 'loose' ? item.remainingWeight : item.remainingQuantity;
            return remaining <= 5 && remaining >= 0 && !isNaN(remaining);
        });

        if (lowStockItems.length === 0) {
            lowStockList.innerHTML = '<p>No items with low stock.</p>';
        } else {
            lowStockList.innerHTML = lowStockItems.map(item => {
                const remaining = item.type === 'loose' ? item.remainingWeight : item.remainingQuantity;
                const unit = item.type === 'loose' ? 'kg' : 'units';
                const index = inventory.indexOf(item);
                return `
                    <p>
                        ${item.name} (Remaining: ${remaining.toFixed(2)}${unit}) - 
                        Price: ₹${item.price.toFixed(2)}/${unit} | 
                        MRP: ₹${(item.mrp || item.price * 1.10).toFixed(2)}/${unit}
                        <button onclick="showStockModal(${index}, 'add')" style="margin-left: 10px; padding: 5px 10px; font-size: 12px; background: #6a0dad; color: white; border: none; border-radius: 5px; cursor: pointer;">Adjust Stock</button>
                    </p>
                `;
            }).join('');
        }
    }

    function showSupportModal() {
        document.getElementById('support-modal').classList.add('active');
    }

    function hideSupportModal() {
        document.getElementById('support-modal').classList.remove('active');
    }

    function showFeedbackModal() {
        document.getElementById('feedback-modal').classList.add('active');
    }

    function hideFeedbackModal() {
        document.getElementById('feedback-modal').classList.remove('active');
    }


// Show AI Support Modal
function showAISupportModal() {
    document.getElementById('ai-support-modal').classList.add('active');
    document.getElementById('chat-input').focus();
    // Debug: Log detailed chat input styles
    const chatInput = document.getElementById('chat-input');
    const computedStyles = window.getComputedStyle(chatInput);
    console.log('Chat Input Height:', computedStyles.height);
    console.log('Chat Input Padding:', computedStyles.padding);
    console.log('Chat Input Font Size:', computedStyles.fontSize);
    console.log('Chat Input Border:', computedStyles.border);
    console.log('Modal Width:', document.getElementById('ai-support-modal').offsetWidth, 'px');
    console.log('Chat Container Height:', document.querySelector('#ai-support-modal .chat-container').offsetHeight, 'px');
}

// Hide AI Support Modal
function hideAISupportModal() {
    document.getElementById('ai-support-modal').classList.remove('active');
    // Clear chat for next session
    const chatContainer = document.getElementById('chat-container');
    chatContainer.innerHTML = '<div class="chat-message bot-message">Hello! How can I assist you today?</div>';
    document.getElementById('chat-input').value = '';
}

// Send Message and Get Response
function sendMessage() {
    const input = document.getElementById('chat-input');
    const message = input.value.trim().toLowerCase();
    if (!message) return;

    // Add user message to chat
    const chatContainer = document.getElementById('chat-container');
    const userMessage = document.createElement('div');
    userMessage.className = 'chat-message user-message';
    userMessage.textContent = message;
    chatContainer.appendChild(userMessage);

    // Clear input
    input.value = '';

    // Scroll to bottom
    chatContainer.scrollTop = chatContainer.scrollHeight;

    // Get bot response
    setTimeout(() => {
        const botMessage = document.createElement('div');
        botMessage.className = 'chat-message bot-message';
        botMessage.textContent = getBotResponse(message);
        chatContainer.appendChild(botMessage);
        chatContainer.scrollTop = chatContainer.scrollHeight;
    }, 500);
}

// Simple keyword-based response system
function getBotResponse(message) {
    message = message.toLowerCase().trim();

    // KiranaKart POS-related queries
    if (message.includes('add item') || message.includes('inventory')) {
        return 'To add an item, go to the "Inventory" tab, select the item type (loose or packet), fill in details like name, price, and quantity/weight, then click "Add to Inventory".';
    } else if (message.includes('edit item') || message.includes('update inventory')) {
        return 'To edit an item, go to the "Inventory" tab, find the item in the list, click "Edit", update the details (e.g., price, quantity), and click "Save".';
    } else if (message.includes('delete item') || message.includes('remove item')) {
        return 'To delete an item, go to the "Inventory" tab, find the item, click "Delete", and confirm the action in the popup.';
    } else if (message.includes('total') || message.includes('cart')) {
        return 'You can see your cart total in the "Billing" tab. Add items to the cart from the "Inventory" tab, and the total will update automatically at the bottom.';
    } else if (message.includes('invoice') || message.includes('generate invoice')) {
        return 'To generate an invoice, go to the "Billing" tab, add items to your cart, and click "Generate Invoice". You can then save or print the invoice.';
    } else if (message.includes('view invoice') || message.includes('invoice history')) {
        return 'To view past invoices, go to the "Transactions" tab, where you can see a list of all generated invoices with details like date, total, and items.';
    } else if (message.includes('refund') || message.includes('return')) {
        return 'To process a refund, go to the "Transactions" tab, find the invoice, click "Refund", select the items to return, and confirm. The stock will be updated automatically.';
    } else if (message.includes('stock') || message.includes('low stock')) {
        return 'Check the "Stock Management" or "Low Stock" tab to see items with low stock (≤ 5 units/kg). You can adjust stock by clicking "Add Stock" or "Edit Stock".';
    } else if (message.includes('report') || message.includes('sales report')) {
        return 'Go to the "Reports" tab and click "View Sales Report" to see your sales data, including a chart and detailed breakdown. You can also clear reports if needed.';
    } else if (message.includes('customer') || message.includes('add customer')) {
        return 'To add a customer, go to the "Customers" tab, click "Add Customer", enter their details (e.g., name, phone number), and save.';
    } else if (message.includes('support') || message.includes('help')) {
        return 'For more help, click the "Support" button to email kiranakartpos@gmail.com, or ask me anything here!';
    } else if (message.includes('feedback')) {
        return 'You can provide feedback by clicking the "Feedback" button in the top-right corner. It will open a pre-filled email to send your thoughts.';
    }

    // Troubleshooting queries
    if (message.includes('login') || message.includes('sign in') || message.includes('can’t log in')) {
        return 'If you can’t log in, ensure you’re using the correct username (e.g., "satgurukirana") and password (e.g., "satguru123"). If you’ve forgotten your password, contact support at kiranakartpos@gmail.com.';
    } else if (message.includes('invoice error') || message.includes('invoice not generating')) {
        return 'If the invoice isn’t generating, ensure you’ve added items to the cart and clicked "Generate Invoice". If the issue persists, check your internet connection or contact support.';
    } else if (message.includes('report wrong') || message.includes('sales report error')) {
        return 'If the sales report looks incorrect, try clearing the reports by clicking "Clear Reports" in the "Reports" tab and generating new transactions. If the issue persists, contact support.';
    } else if (message.includes('stock not updating') || message.includes('inventory error')) {
        return 'If stock isn’t updating, ensure you’ve saved the changes after adding or editing items. If the issue persists, try refreshing the page or contact support.';
    } else if (message.includes('cart empty') || message.includes('cart not working')) {
        return 'If the cart is empty or not working, ensure you’ve added items from the "Inventory" tab. If the issue persists, try refreshing the page or clearing the cart.';
    }

    // General store-related queries
    if (message.includes('store hours') || message.includes('open') || message.includes('close')) {
        return 'Satguru Kirana Store is open from 8 AM to 8 PM daily. If you have specific questions, feel free to ask!';
    } else if (message.includes('location') || message.includes('where') || message.includes('address')) {
        return 'Satguru Kirana Store is located on the main road of your mohalla. For more details, you can contact the store owner.';
    } else if (message.includes('delivery')) {
        return 'Delivery services depend on the store owner’s availability. Please contact support for more information on setting up delivery.';
    } else if (message.includes('product') || message.includes('item available') || message.includes('in stock')) {
        return 'To check if a product is available, go to the "Inventory" tab and search for the item. You can also ask the store owner for specific products.';
    } else if (message.includes('price') || message.includes('cost') || message.includes('how much')) {
        return 'To check the price of an item, go to the "Inventory" tab and look for the item in the list. Prices are displayed next to each item.';
    } else if (message.includes('discount') || message.includes('offer')) {
        return 'Discounts and offers depend on the store owner. You can ask the owner directly or check the "Billing" tab for any applied discounts during checkout.';
    } else if (message.includes('payment') || message.includes('pay')) {
        return 'Satguru Kirana Store accepts cash, UPI, and card payments. You can select your payment method during checkout in the "Billing" tab.';
    } else if (message.includes('loyalty') || message.includes('reward')) {
        return 'Currently, there’s no loyalty program in KiranaKart POS, but you can suggest it to the store owner or through the "Feedback" button!';
    }

    // Fallback for unrecognized queries
    return 'I can help with KiranaKart POS features, troubleshooting, or store-related questions! Try asking about adding items, generating invoices, store hours, product availability, or troubleshooting issues. What else can I assist you with?';
}









    </script>
</body>
</html>
