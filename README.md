<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Task Manager - Calendario Horizontal</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary: #4F46E5;
            --primary-dark: #4338CA;
            --secondary: #10B981;
            --danger: #EF4444;
            --warning: #F59E0B;
            --light: #F9FAFB;
            --dark: #1F2937;
            --gray: #6B7280;
            --light-gray: #E5E7EB;
            --white: #FFFFFF;
            --shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
            --shadow-lg: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
        }
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        body {
            background-color: var(--light);
            color: var(--dark);
            transition: background-color 0.3s, color 0.3s;
        }
        body.dark-mode {
            background-color: var(--dark);
            color: var(--light);
        }
        .container {
            display: flex;
            height: 100vh;
            overflow: hidden;
        }
        /* Sidebar */
        .sidebar {
            width: 260px;
            background-color: var(--white);
            border-right: 1px solid var(--light-gray);
            padding: 20px;
            display: flex;
            flex-direction: column;
            transition: background-color 0.3s;
        }
        body.dark-mode .sidebar {
            background-color: #2D3748;
            border-right-color: #4A5568;
        }
        .logo {
            display: flex;
            align-items: center;
            margin-bottom: 30px;
            font-size: 24px;
            font-weight: 700;
            color: var(--primary);
        }
        .logo i {
            margin-right: 10px;
            font-size: 28px;
        }
        .nav-menu {
            list-style: none;
            margin-bottom: 30px;
        }
        .nav-item {
            margin-bottom: 8px;
        }
        .nav-link {
            display: flex;
            align-items: center;
            padding: 12px 15px;
            border-radius: 8px;
            color: var(--gray);
            text-decoration: none;
            transition: all 0.2s;
            cursor: pointer;
        }
        .nav-link:hover, .nav-link.active {
            background-color: rgba(79, 70, 229, 0.1);
            color: var(--primary);
        }
        body.dark-mode .nav-link:hover, body.dark-mode .nav-link.active {
            background-color: rgba(79, 70, 229, 0.2);
        }
        .nav-link i {
            margin-right: 12px;
            font-size: 18px;
        }
        .filters {
            margin-top: auto;
        }
        .filter-title {
            font-size: 14px;
            font-weight: 600;
            margin-bottom: 12px;
            color: var(--gray);
        }
        .filter-options {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
        }
        .filter-tag {
            padding: 6px 12px;
            background-color: var(--light-gray);
            border-radius: 20px;
            font-size: 13px;
            cursor: pointer;
            transition: all 0.2s;
        }
        .filter-tag:hover {
            background-color: var(--primary);
            color: white;
        }
        body.dark-mode .filter-tag {
            background-color: #4A5568;
        }
        body.dark-mode .filter-tag:hover {
            background-color: var(--primary);
        }
        /* Main Content */
        .main-content {
            flex: 1;
            display: flex;
            flex-direction: column;
            overflow: hidden;
        }
        .header {
            background-color: var(--white);
            padding: 20px 30px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid var(--light-gray);
            transition: background-color 0.3s;
        }
        body.dark-mode .header {
            background-color: #2D3748;
            border-bottom-color: #4A5568;
        }
        .header-left {
            display: flex;
            align-items: center;
        }
        .view-toggle {
            display: flex;
            margin-left: 20px;
            background-color: var(--light-gray);
            border-radius: 8px;
            overflow: hidden;
        }
        body.dark-mode .view-toggle {
            background-color: #4A5568;
        }
        .view-btn {
            padding: 8px 16px;
            background: none;
            border: none;
            cursor: pointer;
            font-size: 14px;
            font-weight: 500;
            color: var(--gray);
            transition: all 0.2s;
        }
        .view-btn.active {
            background-color: var(--primary);
            color: white;
        }
        .header-right {
            display: flex;
            align-items: center;
        }
        .search-box {
            position: relative;
            margin-right: 20px;
        }
        .search-box input {
            padding: 10px 15px 10px 40px;
            border: 1px solid var(--light-gray);
            border-radius: 8px;
            width: 250px;
            background-color: var(--light);
            transition: all 0.2s;
        }
        body.dark-mode .search-box input {
            background-color: #1A202C;
            border-color: #4A5568;
            color: var(--light);
        }
        .search-box i {
            position: absolute;
            left: 15px;
            top: 50%;
            transform: translateY(-50%);
            color: var(--gray);
        }
        .btn {
            padding: 10px 20px;
            border: none;
            border-radius: 8px;
            font-size: 14px;
            font-weight: 600;
            cursor: pointer;
            display: flex;
            align-items: center;
            transition: all 0.2s;
        }
        .btn-primary {
            background-color: var(--primary);
            color: white;
        }
        .btn-primary:hover {
            background-color: var(--primary-dark);
        }
        .btn i {
            margin-right: 8px;
        }
        .theme-toggle {
            margin-left: 15px;
            background: none;
            border: none;
            font-size: 20px;
            color: var(--gray);
            cursor: pointer;
            transition: color 0.2s;
        }
        .theme-toggle:hover {
            color: var(--primary);
        }
        /* Calendar Views */
        .calendar-container {
            flex: 1;
            overflow: hidden;
            padding: 20px 30px;
            background-color: var(--light);
            transition: background-color 0.3s;
            display: flex;
            flex-direction: column;
        }
        body.dark-mode .calendar-container {
            background-color: #1A202C;
        }
        .view-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }
        .date-navigation {
            display: flex;
            align-items: center;
        }
        .date-navigation button {
            background: none;
            border: none;
            font-size: 18px;
            color: var(--gray);
            cursor: pointer;
            padding: 5px 10px;
            border-radius: 4px;
            transition: all 0.2s;
        }
        .date-navigation button:hover {
            background-color: var(--light-gray);
            color: var(--primary);
        }
        body.dark-mode .date-navigation button:hover {
            background-color: #4A5568;
        }
        .current-date {
            font-size: 24px;
            font-weight: 700;
            margin: 0 15px;
        }
        .today-btn {
            padding: 6px 12px;
            background-color: var(--light-gray);
            border: none;
            border-radius: 6px;
            font-size: 14px;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.2s;
        }
        .today-btn:hover {
            background-color: var(--primary);
            color: white;
        }
        body.dark-mode .today-btn {
            background-color: #4A5568;
        }
        /* Horizontal Daily View */
        .daily-view {
            display: flex;
            flex-direction: column;
            height: 100%;
        }
        .daily-timeline {
            display: flex;
            flex-direction: column;
            overflow-x: auto;
            flex: 1;
            border: 1px solid var(--light-gray);
            border-radius: 8px;
            background-color: var(--white);
            position: relative;
        }
        body.dark-mode .daily-timeline {
            background-color: #2D3748;
            border-color: #4A5568;
        }
        .hours-container {
            display: flex;
            min-width: 720px;
            height: 40px;
            border-bottom: 1px solid var(--light-gray);
        }
        body.dark-mode .hours-container {
            border-bottom-color: #4A5568;
        }
        .hour {
            width: 60px;
            text-align: center;
            font-size: 12px;
            color: var(--gray);
            padding: 10px 0;
            border-right: 1px solid var(--light-gray);
        }
        body.dark-mode .hour {
            border-right-color: #4A5568;
        }
        .tasks-container {
            position: relative;
            min-width: 720px;
            flex: 1;
            overflow-y: auto;
        }
        .task-row {
            position: relative;
            height: 80px;
            border-bottom: 1px solid var(--light-gray);
        }
        body.dark-mode .task-row {
            border-bottom-color: #4A5568;
        }
        .task-item {
            position: absolute;
            height: 70px;
            border-radius: 8px;
            padding: 10px;
            box-shadow: var(--shadow);
            cursor: move;
            transition: all 0.2s;
            z-index: 10;
            overflow: hidden;
            top: 5px;
        }
        .task-item:hover {
            box-shadow: var(--shadow-lg);
            transform: translateY(-2px);
        }
        .task-item.dragging {
            opacity: 0.7;
            transform: rotate(2deg);
            z-index: 100;
        }
        .task-header {
            display: flex;
            justify-content: space-between;
            margin-bottom: 5px;
        }
        .task-title {
            font-weight: 600;
            font-size: 14px;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }
        .task-time {
            font-size: 12px;
            color: var(--gray);
        }
        .task-description {
            font-size: 13px;
            color: var(--gray);
            margin-bottom: 8px;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }
        .task-footer {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .task-tags {
            display: flex;
            gap: 5px;
        }
        .task-tag {
            font-size: 11px;
            padding: 3px 8px;
            border-radius: 12px;
            background-color: rgba(255, 255, 255, 0.3);
        }
        .task-priority {
            width: 10px;
            height: 10px;
            border-radius: 50%;
        }
        .priority-high {
            background-color: var(--danger);
        }
        .priority-medium {
            background-color: var(--warning);
        }
        .priority-low {
            background-color: var(--secondary);
        }
        .task-delete {
            background: none;
            border: none;
            color: var(--gray);
            cursor: pointer;
            font-size: 12px;
            padding: 2px;
            margin-left: 5px;
        }
        .task-delete:hover {
            color: var(--danger);
        }
        /* Horizontal Weekly View */
        .weekly-view {
            display: none;
            flex-direction: column;
            height: 100%;
        }
        .weekly-timeline {
            display: flex;
            overflow-x: auto;
            flex: 1;
            border: 1px solid var(--light-gray);
            border-radius: 8px;
            background-color: var(--white);
        }
        body.dark-mode .weekly-timeline {
            background-color: #2D3748;
            border-color: #4A5568;
        }
        .week-header {
            display: flex;
            min-width: 700px;
            height: 40px;
            border-bottom: 1px solid var(--light-gray);
        }
        body.dark-mode .week-header {
            border-bottom-color: #4A5568;
        }
        .day-header {
            width: 100px;
            text-align: center;
            font-weight: 600;
            padding: 10px 0;
            border-right: 1px solid var(--light-gray);
        }
        body.dark-mode .day-header {
            border-right-color: #4A5568;
        }
        .day-header.today {
            color: var(--primary);
        }
        .week-days {
            display: flex;
            min-width: 700px;
            flex: 1;
        }
        .day-column {
            width: 100px;
            border-right: 1px solid var(--light-gray);
            position: relative;
        }
        body.dark-mode .day-column {
            border-right-color: #4A5568;
        }
        .day-column:last-child {
            border-right: none;
        }
        .day-tasks {
            position: relative;
            height: 100%;
        }
        .day-task {
            position: absolute;
            left: 5px;
            right: 5px;
            border-radius: 6px;
            padding: 8px;
            font-size: 12px;
            margin-bottom: 5px;
            box-shadow: var(--shadow);
            overflow: hidden;
            text-overflow: ellipsis;
            white-space: nowrap;
        }
        /* Horizontal Monthly View */
        .monthly-view {
            display: none;
            flex-direction: column;
            height: 100%;
        }
        .month-timeline {
            display: flex;
            overflow-x: auto;
            flex: 1;
            border: 1px solid var(--light-gray);
            border-radius: 8px;
            background-color: var(--white);
        }
        body.dark-mode .month-timeline {
            background-color: #2D3748;
            border-color: #4A5568;
        }
        .month-header {
            display: flex;
            min-width: 1400px;
            height: 40px;
            border-bottom: 1px solid var(--light-gray);
        }
        body.dark-mode .month-header {
            border-bottom-color: #4A5568;
        }
        .month-day-header {
            width: 45px;
            text-align: center;
            font-weight: 600;
            font-size: 12px;
            padding: 10px 0;
            border-right: 1px solid var(--light-gray);
        }
        body.dark-mode .month-day-header {
            border-right-color: #4A5568;
        }
        .month-days {
            display: flex;
            min-width: 1400px;
            flex: 1;
        }
        .month-day-column {
            width: 45px;
            border-right: 1px solid var(--light-gray);
            position: relative;
        }
        body.dark-mode .month-day-column {
            border-right-color: #4A5568;
        }
        .month-day-column:last-child {
            border-right: none;
        }
        .month-day-number {
            text-align: center;
            font-weight: 600;
            padding: 8px 0;
            border-bottom: 1px solid var(--light-gray);
            font-size: 14px;
        }
        body.dark-mode .month-day-number {
            border-bottom-color: #4A5568;
        }
        .month-day-number.today {
            color: var(--primary);
        }
        .month-day-tasks {
            padding: 5px;
        }
        .month-day-task {
            height: 20px;
            border-radius: 4px;
            margin-bottom: 4px;
            background-color: var(--primary);
            color: white;
            font-size: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            overflow: hidden;
            text-overflow: ellipsis;
            white-space: nowrap;
        }
        /* Recurring Tasks View */
        .recurring-view {
            display: none;
            flex-direction: column;
            height: 100%;
        }
        .recurring-tasks-container {
            flex: 1;
            overflow-y: auto;
            border: 1px solid var(--light-gray);
            border-radius: 8px;
            background-color: var(--white);
            padding: 20px;
        }
        body.dark-mode .recurring-tasks-container {
            background-color: #2D3748;
            border-color: #4A5568;
        }
        .recurring-task-item {
            background-color: var(--light);
            border-radius: 8px;
            padding: 15px;
            margin-bottom: 15px;
            box-shadow: var(--shadow);
            transition: all 0.2s;
        }
        body.dark-mode .recurring-task-item {
            background-color: #1A202C;
        }
        .recurring-task-item:hover {
            box-shadow: var(--shadow-lg);
            transform: translateY(-2px);
        }
        .recurring-task-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
        }
        .recurring-task-title {
            font-size: 18px;
            font-weight: 600;
        }
        .recurring-task-actions {
            display: flex;
            gap: 10px;
        }
        .recurring-task-description {
            color: var(--gray);
            margin-bottom: 10px;
        }
        .recurring-task-footer {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .recurring-task-tags {
            display: flex;
            gap: 5px;
        }
        .recurring-task-tag {
            font-size: 12px;
            padding: 4px 10px;
            border-radius: 20px;
            background-color: var(--primary);
            color: white;
        }
        .btn-small {
            padding: 6px 12px;
            font-size: 12px;
        }
        /* Task Modal */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            z-index: 1000;
            justify-content: center;
            align-items: center;
        }
        .modal-content {
            background-color: var(--white);
            border-radius: 12px;
            width: 90%;
            max-width: 600px;
            max-height: 90vh;
            overflow-y: auto;
            box-shadow: var(--shadow-lg);
            animation: modalFadeIn 0.3s;
        }
        body.dark-mode .modal-content {
            background-color: #2D3748;
        }
        @keyframes modalFadeIn {
            from {
                opacity: 0;
                transform: translateY(-20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        .modal-header {
            padding: 20px;
            border-bottom: 1px solid var(--light-gray);
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        body.dark-mode .modal-header {
            border-bottom-color: #4A5568;
        }
        .modal-title {
            font-size: 20px;
            font-weight: 700;
        }
        .modal-close {
            background: none;
            border: none;
            font-size: 24px;
            color: var(--gray);
            cursor: pointer;
            transition: color 0.2s;
        }
        .modal-close:hover {
            color: var(--danger);
        }
        .modal-body {
            padding: 20px;
        }
        .form-group {
            margin-bottom: 20px;
        }
        .form-label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            font-size: 14px;
        }
        .form-control {
            width: 100%;
            padding: 12px;
            border: 1px solid var(--light-gray);
            border-radius: 8px;
            font-size: 14px;
            background-color: var(--light);
            transition: all 0.2s;
        }
        body.dark-mode .form-control {
            background-color: #1A202C;
            border-color: #4A5568;
            color: var(--light);
        }
        .form-control:focus {
            outline: none;
            border-color: var(--primary);
            box-shadow: 0 0 0 3px rgba(79, 70, 229, 0.1);
        }
        .form-row {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
        }
        .priority-selector {
            display: flex;
            gap: 10px;
        }
        .priority-option {
            flex: 1;
            padding: 10px;
            border: 1px solid var(--light-gray);
            border-radius: 8px;
            text-align: center;
            cursor: pointer;
            transition: all 0.2s;
        }
        body.dark-mode .priority-option {
            border-color: #4A5568;
        }
        .priority-option:hover {
            border-color: var(--primary);
        }
        .priority-option.selected {
            background-color: var(--primary);
            color: white;
            border-color: var(--primary);
        }
        .tag-input-container {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
            padding: 8px;
            border: 1px solid var(--light-gray);
            border-radius: 8px;
            min-height: 45px;
        }
        body.dark-mode .tag-input-container {
            border-color: #4A5568;
        }
        .tag-item {
            display: flex;
            align-items: center;
            background-color: var(--primary);
            color: white;
            padding: 4px 10px;
            border-radius: 20px;
            font-size: 13px;
        }
        .tag-item button {
            background: none;
            border: none;
            color: white;
            margin-left: 6px;
            cursor: pointer;
            font-size: 14px;
        }
        .tag-input {
            flex: 1;
            border: none;
            background: none;
            outline: none;
            min-width: 100px;
            color: var(--dark);
        }
        body.dark-mode .tag-input {
            color: var(--light);
        }
        .subtasks-container {
            margin-top: 10px;
        }
        .subtask-item {
            display: flex;
            align-items: center;
            padding: 10px;
            border: 1px solid var(--light-gray);
            border-radius: 8px;
            margin-bottom: 8px;
        }
        body.dark-mode .subtask-item {
            border-color: #4A5568;
        }
        .subtask-checkbox {
            margin-right: 10px;
        }
        .subtask-text {
            flex: 1;
        }
        .subtask-remove {
            background: none;
            border: none;
            color: var(--danger);
            cursor: pointer;
        }
        .add-subtask {
            display: flex;
            margin-top: 10px;
        }
        .add-subtask input {
            flex: 1;
            border: 1px solid var(--light-gray);
            border-radius: 8px 0 0 8px;
            padding: 10px;
        }
        body.dark-mode .add-subtask input {
            border-color: #4A5568;
            background-color: #1A202C;
            color: var(--light);
        }
        .add-subtask button {
            padding: 10px 15px;
            background-color: var(--primary);
            color: white;
            border: none;
            border-radius: 0 8px 8px 0;
            cursor: pointer;
        }
        .modal-footer {
            padding: 15px 20px;
            border-top: 1px solid var(--light-gray);
            display: flex;
            justify-content: flex-end;
            gap: 10px;
        }
        body.dark-mode .modal-footer {
            border-top-color: #4A5568;
        }
        .btn-secondary {
            background-color: var(--light-gray);
            color: var(--dark);
        }
        body.dark-mode .btn-secondary {
            background-color: #4A5568;
            color: var(--light);
        }
        .recurring-options {
            margin-top: 15px;
            padding-top: 15px;
            border-top: 1px solid var(--light-gray);
        }
        body.dark-mode .recurring-options {
            border-top-color: #4A5568;
        }
        .form-check {
            display: flex;
            align-items: center;
            margin-bottom: 10px;
        }
        .form-check-input {
            margin-right: 10px;
        }
        /* Stats View */
        .stats-container {
            display: flex;
            gap: 20px;
            flex-wrap: wrap;
        }
        .stat-card {
            background-color: var(--white);
            border-radius: 12px;
            padding: 20px;
            box-shadow: var(--shadow);
            flex: 1;
            min-width: 200px;
            text-align: center;
        }
        body.dark-mode .stat-card {
            background-color: #2D3748;
        }
        .stat-card h3 {
            margin-bottom: 15px;
            color: var(--gray);
            font-size: 16px;
        }
        .stat-value {
            font-size: 36px;
            font-weight: 700;
            color: var(--primary);
        }
        /* Responsive */
        @media (max-width: 768px) {
            .sidebar {
                position: fixed;
                left: -260px;
                height: 100%;
                z-index: 100;
                box-shadow: var(--shadow-lg);
            }
            .sidebar.open {
                left: 0;
            }
            .menu-toggle {
                display: block;
                margin-right: 15px;
                background: none;
                border: none;
                font-size: 20px;
                color: var(--gray);
                cursor: pointer;
            }
            .header-left {
                width: 100%;
            }
            .search-box {
                display: none;
            }
            .view-toggle {
                margin-left: auto;
            }
            .daily-timeline,
            .weekly-timeline,
            .month-timeline {
                flex-direction: column;
            }
            .hours-container,
            .week-header,
            .month-header {
                min-width: 100%;
                overflow-x: auto;
            }
            .tasks-container,
            .week-days,
            .month-days {
                min-width: 100%;
                overflow-x: auto;
            }
        }
        @media (min-width: 769px) {
            .menu-toggle {
                display: none;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Sidebar -->
        <aside class="sidebar" id="sidebar">
            <div class="logo">
                <i class="fas fa-calendar-check"></i>
                <span>TaskFlow</span>
            </div>
            
            <ul class="nav-menu">
                <li class="nav-item">
                    <a href="#" class="nav-link active" data-view="daily">
                        <i class="fas fa-calendar-day"></i>
                        <span>Día</span>
                    </a>
                </li>
                <li class="nav-item">
                    <a href="#" class="nav-link" data-view="weekly">
                        <i class="fas fa-calendar-week"></i>
                        <span>Semana</span>
                    </a>
                </li>
                <li class="nav-item">
                    <a href="#" class="nav-link" data-view="monthly">
                        <i class="fas fa-calendar-alt"></i>
                        <span>Mes</span>
                    </a>
                </li>
                <li class="nav-item">
                    <a href="#" class="nav-link" data-view="recurring">
                        <i class="fas fa-sync-alt"></i>
                        <span>Tareas Repetitivas</span>
                    </a>
                </li>
                <li class="nav-item">
                    <a href="#" class="nav-link" data-view="tasks">
                        <i class="fas fa-tasks"></i>
                        <span>Tareas</span>
                    </a>
                </li>
                <li class="nav-item">
                    <a href="#" class="nav-link" data-view="stats">
                        <i class="fas fa-chart-bar"></i>
                        <span>Estadísticas</span>
                    </a>
                </li>
            </ul>
            
            <div class="filters">
                <h3 class="filter-title">Filtros rápidos</h3>
                <div class="filter-options">
                    <div class="filter-tag">Pendientes</div>
                    <div class="filter-tag">En progreso</div>
                    <div class="filter-tag">Completadas</div>
                    <div class="filter-tag">Alta prioridad</div>
                    <div class="filter-tag">Trabajo</div>
                    <div class="filter-tag">Personal</div>
                </div>
            </div>
        </aside>
        
        <!-- Main Content -->
        <main class="main-content">
            <!-- Header -->
            <header class="header">
                <div class="header-left">
                    <button class="menu-toggle" id="menuToggle">
                        <i class="fas fa-bars"></i>
                    </button>
                    <div class="view-toggle">
                        <button class="view-btn active" data-view="daily">Día</button>
                        <button class="view-btn" data-view="weekly">Semana</button>
                        <button class="view-btn" data-view="monthly">Mes</button>
                    </div>
                </div>
                
                <div class="header-right">
                    <div class="search-box">
                        <i class="fas fa-search"></i>
                        <input type="text" placeholder="Buscar tareas...">
                    </div>
                    <button class="btn btn-primary" id="addTaskBtn">
                        <i class="fas fa-plus"></i>
                        <span>Agregar Tarea</span>
                    </button>
                    <button class="theme-toggle" id="themeToggle">
                        <i class="fas fa-moon"></i>
                    </button>
                </div>
            </header>
            
            <!-- Calendar Container -->
            <div class="calendar-container">
                <!-- Daily View -->
                <div class="daily-view" id="dailyView">
                    <div class="view-header">
                        <div class="date-navigation">
                            <button id="prevDay">
                                <i class="fas fa-chevron-left"></i>
                            </button>
                            <div class="current-date" id="currentDate">Hoy, 15 de junio de 2023</div>
                            <button id="nextDay">
                                <i class="fas fa-chevron-right"></i>
                            </button>
                        </div>
                        <button class="today-btn">Hoy</button>
                    </div>
                    
                    <div class="daily-timeline">
                        <div class="hours-container" id="hoursContainer">
                            <!-- Hours will be generated by JavaScript -->
                        </div>
                        <div class="tasks-container" id="tasksContainer">
                            <!-- Tasks will be added here dynamically -->
                        </div>
                    </div>
                </div>
                
                <!-- Weekly View -->
                <div class="weekly-view" id="weeklyView">
                    <div class="view-header">
                        <div class="date-navigation">
                            <button id="prevWeek">
                                <i class="fas fa-chevron-left"></i>
                            </button>
                            <div class="current-date" id="currentWeek">12 - 18 de junio de 2023</div>
                            <button id="nextWeek">
                                <i class="fas fa-chevron-right"></i>
                            </button>
                        </div>
                        <button class="today-btn">Hoy</button>
                    </div>
                    
                    <div class="weekly-timeline">
                        <div class="week-header" id="weekHeader">
                            <!-- Week days will be generated by JavaScript -->
                        </div>
                        <div class="week-days" id="weekDays">
                            <!-- Week days columns will be generated by JavaScript -->
                        </div>
                    </div>
                </div>
                
                <!-- Monthly View -->
                <div class="monthly-view" id="monthlyView">
                    <div class="view-header">
                        <div class="date-navigation">
                            <button id="prevMonth">
                                <i class="fas fa-chevron-left"></i>
                            </button>
                            <div class="current-date" id="currentMonth">Junio 2023</div>
                            <button id="nextMonth">
                                <i class="fas fa-chevron-right"></i>
                            </button>
                        </div>
                        <button class="today-btn">Hoy</button>
                    </div>
                    
                    <div class="month-timeline">
                        <div class="month-header" id="monthHeader">
                            <!-- Month days will be generated by JavaScript -->
                        </div>
                        <div class="month-days" id="monthDays">
                            <!-- Month days columns will be generated by JavaScript -->
                        </div>
                    </div>
                </div>
                
                <!-- Recurring Tasks View -->
                <div class="recurring-view" id="recurringView">
                    <div class="view-header">
                        <h2>Tareas Repetitivas</h2>
                        <button class="btn btn-primary" id="addRecurringTaskBtn">
                            <i class="fas fa-plus"></i>
                            <span>Agregar Tarea Repetitiva</span>
                        </button>
                    </div>
                    
                    <div class="recurring-tasks-container" id="recurringTasksContainer">
                        <!-- Recurring tasks will be added here dynamically -->
                    </div>
                </div>
                
                <!-- Tasks List View -->
                <div class="tasks-view" id="tasksView">
                    <div class="view-header">
                        <h2>Lista de Tareas</h2>
                        <button class="btn btn-primary" id="addTaskFromListBtn">
                            <i class="fas fa-plus"></i>
                            <span>Agregar Tarea</span>
                        </button>
                    </div>
                    
                    <div class="tasks-list-container" id="tasksListContainer">
                        <!-- Tasks list will be added here dynamically -->
                    </div>
                </div>
                
                <!-- Stats View -->
                <div class="stats-view" id="statsView">
                    <div class="view-header">
                        <h2>Estadísticas</h2>
                    </div>
                    
                    <div class="stats-container">
                        <div class="stat-card">
                            <h3>Tareas Completadas</h3>
                            <div class="stat-value" id="completedTasksCount">0</div>
                        </div>
                        <div class="stat-card">
                            <h3>Tareas Pendientes</h3>
                            <div class="stat-value" id="pendingTasksCount">0</div>
                        </div>
                        <div class="stat-card">
                            <h3>Tareas de Alta Prioridad</h3>
                            <div class="stat-value" id="highPriorityTasksCount">0</div>
                        </div>
                    </div>
                </div>
            </div>
        </main>
    </div>
    
    <!-- Task Modal -->
    <div class="modal" id="taskModal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 class="modal-title" id="modalTitle">Nueva Tarea</h2>
                <button class="modal-close" id="modalClose">
                    <i class="fas fa-times"></i>
                </button>
            </div>
            
            <div class="modal-body">
                <form id="taskForm">
                    <div class="form-group">
                        <label class="form-label">Título</label>
                        <input type="text" class="form-control" id="taskTitle" placeholder="Nombre de la tarea" required>
                    </div>
                    
                    <div class="form-group">
                        <label class="form-label">Descripción</label>
                        <textarea class="form-control" id="taskDescription" rows="3" placeholder="Descripción de la tarea"></textarea>
                    </div>
                    
                    <div class="form-row" id="dateTimeRow">
                        <div class="form-group">
                            <label class="form-label">Fecha</label>
                            <input type="date" class="form-control" id="taskDate" required>
                        </div>
                        
                        <div class="form-group">
                            <label class="form-label">Hora</label>
                            <input type="time" class="form-control" id="taskTime" required>
                        </div>
                    </div>
                    
                    <div class="form-row">
                        <div class="form-group">
                            <label class="form-label">Duración (minutos)</label>
                            <input type="number" class="form-control" id="taskDuration" placeholder="30" min="15" step="15">
                        </div>
                        
                        <div class="form-group">
                            <label class="form-label">Prioridad</label>
                            <div class="priority-selector">
                                <div class="priority-option" data-priority="low">
                                    <i class="fas fa-flag priority-low"></i> Baja
                                </div>
                                <div class="priority-option selected" data-priority="medium">
                                    <i class="fas fa-flag priority-medium"></i> Media
                                </div>
                                <div class="priority-option" data-priority="high">
                                    <i class="fas fa-flag priority-high"></i> Alta
                                </div>
                            </div>
                        </div>
                    </div>
                    
                    <div class="form-group">
                        <label class="form-label">Etiquetas</label>
                        <div class="tag-input-container" id="tagInputContainer">
                            <input type="text" class="tag-input" id="tagInput" placeholder="Añadir etiqueta">
                        </div>
                    </div>
                    
                    <div class="form-group">
                        <label class="form-label">Recordatorios</label>
                        <select class="form-control" id="taskReminder">
                            <option value="none">Sin recordatorio</option>
                            <option value="10">10 minutos antes</option>
                            <option value="30">30 minutos antes</option>
                            <option value="60">1 hora antes</option>
                            <option value="1440">1 día antes</option>
                        </select>
                    </div>
                    
                    <div class="recurring-options" id="recurringOptions" style="display: none;">
                        <div class="form-check">
                            <input type="checkbox" class="form-check-input" id="isRecurring">
                            <label class="form-check-label" for="isRecurring">Es una tarea repetitiva</label>
                        </div>
                        
                        <div class="form-group" id="recurringFrequencyGroup" style="display: none;">
                            <label class="form-label">Frecuencia</label>
                            <select class="form-control" id="recurringFrequency">
                                <option value="daily">Diaria</option>
                                <option value="weekly">Semanal</option>
                                <option value="monthly">Mensual</option>
                            </select>
                        </div>
                    </div>
                    
                    <div class="form-group">
                        <label class="form-label">Subtareas</label>
                        <div class="subtasks-container" id="subtasksContainer">
                            <!-- Subtasks will be added here -->
                        </div>
                        <div class="add-subtask">
                            <input type="text" class="form-control" id="newSubtask" placeholder="Añadir subtarea">
                            <button type="button" id="addSubtaskBtn">
                                <i class="fas fa-plus"></i>
                            </button>
                        </div>
                    </div>
                </form>
            </div>
            
            <div class="modal-footer">
                <button class="btn btn-secondary" id="cancelBtn">Cancelar</button>
                <button class="btn btn-primary" id="saveTaskBtn">Guardar Tarea</button>
            </div>
        </div>
    </div>
    
    <script>
        // Global variables
        const app = {
            currentDate: new Date(),
            currentView: 'daily',
            tasks: [],
            recurringTasks: [],
            tags: [],
            selectedPriority: 'medium',
            draggedTask: null,
            isRecurringTask: false,
            elements: {
                dailyView: document.getElementById('dailyView'),
                weeklyView: document.getElementById('weeklyView'),
                monthlyView: document.getElementById('monthlyView'),
                recurringView: document.getElementById('recurringView'),
                tasksView: document.getElementById('tasksView'),
                statsView: document.getElementById('statsView'),
                hoursContainer: document.getElementById('hoursContainer'),
                tasksContainer: document.getElementById('tasksContainer'),
                weekHeader: document.getElementById('weekHeader'),
                weekDays: document.getElementById('weekDays'),
                monthHeader: document.getElementById('monthHeader'),
                monthDays: document.getElementById('monthDays'),
                recurringTasksContainer: document.getElementById('recurringTasksContainer'),
                tasksListContainer: document.getElementById('tasksListContainer'),
                taskModal: document.getElementById('taskModal'),
                taskForm: document.getElementById('taskForm'),
                sidebar: document.getElementById('sidebar'),
                themeToggle: document.getElementById('themeToggle'),
                modalTitle: document.getElementById('modalTitle'),
                dateTimeRow: document.getElementById('dateTimeRow'),
                recurringOptions: document.getElementById('recurringOptions'),
                isRecurringCheckbox: document.getElementById('isRecurring'),
                recurringFrequencyGroup: document.getElementById('recurringFrequencyGroup')
            }
        };

        // Initialize the app
        document.addEventListener('DOMContentLoaded', () => {
            app.initializeApp();
            app.generateHours();
            app.generateWeekDays();
            app.generateMonthDays();
            app.updateDateDisplay();
            app.setupEventListeners();
            app.loadTasks();
            app.loadRecurringTasks();
            app.updateStats();
        });

        // App methods
        app.initializeApp = function() {
            // Check for dark mode preference
            if (localStorage.getItem('darkMode') === 'true') {
                document.body.classList.add('dark-mode');
                app.elements.themeToggle.innerHTML = '<i class="fas fa-sun"></i>';
            }
            
            // Set today's date as default
            const today = new Date();
            document.getElementById('taskDate').valueAsDate = today;
        };

        app.setupEventListeners = function() {
            // View toggle buttons
            document.querySelectorAll('.view-btn').forEach(btn => {
                btn.addEventListener('click', () => {
                    const view = btn.getAttribute('data-view');
                    app.switchView(view);
                });
            });
            
            // Navigation links
            document.querySelectorAll('.nav-link').forEach(link => {
                link.addEventListener('click', (e) => {
                    e.preventDefault();
                    const view = link.getAttribute('data-view');
                    app.switchView(view);
                });
            });
            
            // Navigation buttons
            document.getElementById('prevDay').addEventListener('click', () => {
                app.currentDate.setDate(app.currentDate.getDate() - 1);
                app.updateDateDisplay();
                app.renderDailyTasks();
            });
            
            document.getElementById('nextDay').addEventListener('click', () => {
                app.currentDate.setDate(app.currentDate.getDate() + 1);
                app.updateDateDisplay();
                app.renderDailyTasks();
            });
            
            document.getElementById('prevWeek').addEventListener('click', () => {
                app.currentDate.setDate(app.currentDate.getDate() - 7);
                app.updateDateDisplay();
                app.renderWeeklyTasks();
            });
            
            document.getElementById('nextWeek').addEventListener('click', () => {
                app.currentDate.setDate(app.currentDate.getDate() + 7);
                app.updateDateDisplay();
                app.renderWeeklyTasks();
            });
            
            document.getElementById('prevMonth').addEventListener('click', () => {
                app.currentDate.setMonth(app.currentDate.getMonth() - 1);
                app.updateDateDisplay();
                app.generateMonthDays();
                app.renderMonthlyTasks();
            });
            
            document.getElementById('nextMonth').addEventListener('click', () => {
                app.currentDate.setMonth(app.currentDate.getMonth() + 1);
                app.updateDateDisplay();
                app.generateMonthDays();
                app.renderMonthlyTasks();
            });
            
            // Today buttons
            document.querySelectorAll('.today-btn').forEach(btn => {
                btn.addEventListener('click', () => {
                    app.currentDate = new Date();
                    app.updateDateDisplay();
                    if (app.currentView === 'daily') {
                        app.renderDailyTasks();
                    } else if (app.currentView === 'weekly') {
                        app.renderWeeklyTasks();
                    } else if (app.currentView === 'monthly') {
                        app.generateMonthDays();
                        app.renderMonthlyTasks();
                    }
                });
            });
            
            // Task modal
            document.getElementById('addTaskBtn').addEventListener('click', () => {
                app.openTaskModal(false);
            });
            
            document.getElementById('addRecurringTaskBtn').addEventListener('click', () => {
                app.openTaskModal(true);
            });
            
            document.getElementById('addTaskFromListBtn').addEventListener('click', () => {
                app.openTaskModal(false);
            });
            
            document.getElementById('modalClose').addEventListener('click', () => {
                app.closeTaskModal();
            });
            
            document.getElementById('cancelBtn').addEventListener('click', () => {
                app.closeTaskModal();
            });
            
            document.getElementById('saveTaskBtn').addEventListener('click', () => {
                app.saveTask();
            });
            
            // Priority selector
            document.querySelectorAll('.priority-option').forEach(option => {
                option.addEventListener('click', () => {
                    document.querySelectorAll('.priority-option').forEach(opt => {
                        opt.classList.remove('selected');
                    });
                    option.classList.add('selected');
                    app.selectedPriority = option.getAttribute('data-priority');
                });
            });
            
            // Tag input
            const tagInput = document.getElementById('tagInput');
            tagInput.addEventListener('keydown', (e) => {
                if (e.key === 'Enter') {
                    e.preventDefault();
                    app.addTag(tagInput.value.trim());
                    tagInput.value = '';
                }
            });
            
            // Subtask input
            document.getElementById('addSubtaskBtn').addEventListener('click', () => {
                const subtaskText = document.getElementById('newSubtask').value.trim();
                if (subtaskText) {
                    app.addSubtask(subtaskText);
                    document.getElementById('newSubtask').value = '';
                }
            });
            
            document.getElementById('newSubtask').addEventListener('keydown', (e) => {
                if (e.key === 'Enter') {
                    e.preventDefault();
                    const subtaskText = e.target.value.trim();
                    if (subtaskText) {
                        app.addSubtask(subtaskText);
                        e.target.value = '';
                    }
                }
            });
            
            // Theme toggle
            app.elements.themeToggle.addEventListener('click', () => {
                document.body.classList.toggle('dark-mode');
                const isDarkMode = document.body.classList.contains('dark-mode');
                localStorage.setItem('darkMode', isDarkMode);
                app.elements.themeToggle.innerHTML = isDarkMode ? '<i class="fas fa-sun"></i>' : '<i class="fas fa-moon"></i>';
            });
            
            // Mobile menu toggle
            document.getElementById('menuToggle').addEventListener('click', () => {
                app.elements.sidebar.classList.toggle('open');
            });
            
            // Filter tags
            document.querySelectorAll('.filter-tag').forEach(tag => {
                tag.addEventListener('click', () => {
                    tag.classList.toggle('active');
                });
            });
            
            // Recurring task checkbox
            app.elements.isRecurringCheckbox.addEventListener('change', () => {
                if (app.elements.isRecurringCheckbox.checked) {
                    app.elements.recurringFrequencyGroup.style.display = 'block';
                } else {
                    app.elements.recurringFrequencyGroup.style.display = 'none';
                }
            });
        };

        app.switchView = function(view) {
            app.currentView = view;
            
            // Update active button
            document.querySelectorAll('.view-btn').forEach(btn => {
                btn.classList.remove('active');
                if (btn.getAttribute('data-view') === view) {
                    btn.classList.add('active');
                }
            });
            
            // Update nav links
            document.querySelectorAll('.nav-link').forEach(link => {
                link.classList.remove('active');
                if (link.getAttribute('data-view') === view) {
                    link.classList.add('active');
                }
            });
            
            // Show/hide views
            app.elements.dailyView.style.display = view === 'daily' ? 'flex' : 'none';
            app.elements.weeklyView.style.display = view === 'weekly' ? 'flex' : 'none';
            app.elements.monthlyView.style.display = view === 'monthly' ? 'flex' : 'none';
            app.elements.recurringView.style.display = view === 'recurring' ? 'flex' : 'none';
            app.elements.tasksView.style.display = view === 'tasks' ? 'flex' : 'none';
            app.elements.statsView.style.display = view === 'stats' ? 'flex' : 'none';
            
            // Update date display
            app.updateDateDisplay();
            
            // Render tasks for the current view
            if (view === 'daily') {
                app.renderDailyTasks();
            } else if (view === 'weekly') {
                app.renderWeeklyTasks();
            } else if (view === 'monthly') {
                app.renderMonthlyTasks();
            } else if (view === 'recurring') {
                app.renderRecurringTasks();
            } else if (view === 'tasks') {
                app.renderTasksList();
            } else if (view === 'stats') {
                app.updateStats();
            }
        };

        app.updateDateDisplay = function() {
            const options = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' };
            const dateStr = app.currentDate.toLocaleDateString('es-ES', options);
            
            // Capitalize first letter
            const formattedDate = dateStr.charAt(0).toUpperCase() + dateStr.slice(1);
            
            document.getElementById('currentDate').textContent = formattedDate;
            
            // Week display
            const startOfWeek = new Date(app.currentDate);
            startOfWeek.setDate(app.currentDate.getDate() - app.currentDate.getDay() + 1);
            const endOfWeek = new Date(startOfWeek);
            endOfWeek.setDate(startOfWeek.getDate() + 6);
            
            const weekStr = `${startOfWeek.getDate()} - ${endOfWeek.getDate()} de ${startOfWeek.toLocaleDateString('es-ES', { month: 'long' })} ${startOfWeek.getFullYear()}`;
            document.getElementById('currentWeek').textContent = weekStr;
            
            // Month display
            const monthStr = app.currentDate.toLocaleDateString('es-ES', { month: 'long', year: 'numeric' });
            document.getElementById('currentMonth').textContent = monthStr.charAt(0).toUpperCase() + monthStr.slice(1);
        };

        app.generateHours = function() {
            app.elements.hoursContainer.innerHTML = '';
            
            // Generate hours from 6 am to 6 pm
            for (let i = 6; i <= 18; i++) {
                const hour = document.createElement('div');
                hour.className = 'hour';
                hour.textContent = `${i.toString().padStart(2, '0')}:00`;
                app.elements.hoursContainer.appendChild(hour);
            }
        };

        app.generateWeekDays = function() {
            app.elements.weekHeader.innerHTML = '';
            app.elements.weekDays.innerHTML = '';
            
            const days = ['Lun', 'Mar', 'Mié', 'Jue', 'Vie', 'Sáb', 'Dom'];
            const today = new Date();
            
            // Get start of week (Monday)
            const startOfWeek = new Date(app.currentDate);
            startOfWeek.setDate(app.currentDate.getDate() - app.currentDate.getDay() + 1);
            
            for (let i = 0; i < 7; i++) {
                const dayDate = new Date(startOfWeek);
                dayDate.setDate(startOfWeek.getDate() + i);
                
                // Day header
                const dayHeader = document.createElement('div');
                dayHeader.className = 'day-header';
                
                // Check if this is today
                if (dayDate.toDateString() === today.toDateString()) {
                    dayHeader.classList.add('today');
                }
                
                dayHeader.textContent = `${days[i]} ${dayDate.getDate()}`;
                app.elements.weekHeader.appendChild(dayHeader);
                
                // Day column
                const dayColumn = document.createElement('div');
                dayColumn.className = 'day-column';
                dayColumn.dataset.date = dayDate.toISOString().split('T')[0];
                
                const dayTasks = document.createElement('div');
                dayTasks.className = 'day-tasks';
                dayColumn.appendChild(dayTasks);
                
                app.elements.weekDays.appendChild(dayColumn);
            }
        };

        app.generateMonthDays = function() {
            app.elements.monthHeader.innerHTML = '';
            app.elements.monthDays.innerHTML = '';
            
            const year = app.currentDate.getFullYear();
            const month = app.currentDate.getMonth();
            const today = new Date();
            
            // Get first day of month
            const firstDay = new Date(year, month, 1);
            // Get last day of month
            const lastDay = new Date(year, month + 1, 0);
            
            // Add day headers
            const days = ['Dom', 'Lun', 'Mar', 'Mié', 'Jue', 'Vie', 'Sáb'];
            for (let i = 0; i < 7; i++) {
                const dayHeader = document.createElement('div');
                dayHeader.className = 'month-day-header';
                dayHeader.textContent = days[i];
                app.elements.monthHeader.appendChild(dayHeader);
            }
            
            // Add empty cells for days before the first day of the month
            const firstDayOfWeek = firstDay.getDay();
            for (let i = 0; i < firstDayOfWeek; i++) {
                const emptyDay = document.createElement('div');
                emptyDay.className = 'month-day-column';
                app.elements.monthDays.appendChild(emptyDay);
            }
            
            // Add days of the month
            for (let day = 1; day <= lastDay.getDate(); day++) {
                const dayElement = document.createElement('div');
                dayElement.className = 'month-day-column';
                dayElement.dataset.date = `${year}-${(month + 1).toString().padStart(2, '0')}-${day.toString().padStart(2, '0')}`;
                
                const dayNumber = document.createElement('div');
                dayNumber.className = 'month-day-number';
                
                // Check if this is today
                if (year === today.getFullYear() && month === today.getMonth() && day === today.getDate()) {
                    dayNumber.classList.add('today');
                }
                
                dayNumber.textContent = day;
                dayElement.appendChild(dayNumber);
                
                const dayTasks = document.createElement('div');
                dayTasks.className = 'month-day-tasks';
                dayElement.appendChild(dayTasks);
                
                app.elements.monthDays.appendChild(dayElement);
            }
        };

        app.openTaskModal = function(isRecurring) {
            app.isRecurringTask = isRecurring;
            
            if (isRecurring) {
                app.elements.modalTitle.textContent = 'Nueva Tarea Repetitiva';
                app.elements.dateTimeRow.style.display = 'none';
                app.elements.recurringOptions.style.display = 'block';
                app.elements.isRecurringCheckbox.checked = true;
                app.elements.recurringFrequencyGroup.style.display = 'block';
            } else {
                app.elements.modalTitle.textContent = 'Nueva Tarea';
                app.elements.dateTimeRow.style.display = 'grid';
                app.elements.recurringOptions.style.display = 'none';
                app.elements.isRecurringCheckbox.checked = false;
                app.elements.recurringFrequencyGroup.style.display = 'none';
            }
            
            app.elements.taskModal.style.display = 'flex';
            document.getElementById('taskTitle').focus();
        };

        app.closeTaskModal = function() {
            app.elements.taskModal.style.display = 'none';
            app.elements.taskForm.reset();
            app.tags = [];
            app.selectedPriority = 'medium';
            document.getElementById('tagInputContainer').innerHTML = '<input type="text" class="tag-input" id="tagInput" placeholder="Añadir etiqueta">';
            document.getElementById('subtasksContainer').innerHTML = '';
            
            // Reset priority selector
            document.querySelectorAll('.priority-option').forEach(opt => {
                opt.classList.remove('selected');
            });
            document.querySelector('.priority-option[data-priority="medium"]').classList.add('selected');
        };

        app.addTag = function(tagText) {
            if (tagText && !app.tags.includes(tagText)) {
                app.tags.push(tagText);
                app.renderTags();
            }
        };

        app.renderTags = function() {
            const container = document.getElementById('tagInputContainer');
            container.innerHTML = '';
            
            app.tags.forEach(tag => {
                const tagElement = document.createElement('div');
                tagElement.className = 'tag-item';
                tagElement.innerHTML = `
                    ${tag}
                    <button type="button" onclick="app.removeTag('${tag}')">
                        <i class="fas fa-times"></i>
                    </button>
                `;
                container.appendChild(tagElement);
            });
            
            const input = document.createElement('input');
            input.type = 'text';
            input.className = 'tag-input';
            input.id = 'tagInput';
            input.placeholder = 'Añadir etiqueta';
            input.addEventListener('keydown', (e) => {
                if (e.key === 'Enter') {
                    e.preventDefault();
                    app.addTag(input.value.trim());
                    input.value = '';
                }
            });
            container.appendChild(input);
            input.focus();
        };

        app.removeTag = function(tagText) {
            app.tags = app.tags.filter(tag => tag !== tagText);
            app.renderTags();
        };

        app.addSubtask = function(subtaskText) {
            const container = document.getElementById('subtasksContainer');
            const subtaskItem = document.createElement('div');
            subtaskItem.className = 'subtask-item';
            
            const subtaskId = 'subtask-' + Date.now();
            subtaskItem.innerHTML = `
                <input type="checkbox" class="subtask-checkbox" id="${subtaskId}">
                <div class="subtask-text">${subtaskText}</div>
                <button type="button" class="subtask-remove" onclick="app.removeSubtask(this)">
                    <i class="fas fa-trash"></i>
                </button>
            `;
            
            container.appendChild(subtaskItem);
        };

        app.removeSubtask = function(button) {
            button.parentElement.remove();
        };

        app.saveTask = function() {
            const title = document.getElementById('taskTitle').value.trim();
            if (!title) {
                alert('Por favor, introduce un título para la tarea');
                return;
            }
            
            const description = document.getElementById('taskDescription').value.trim();
            const date = document.getElementById('taskDate').value;
            const time = document.getElementById('taskTime').value;
            const duration = parseInt(document.getElementById('taskDuration').value) || 30;
            const priority = app.selectedPriority;
            const reminder = document.getElementById('taskReminder').value;
            
            // Collect subtasks
            const subtasks = [];
            document.querySelectorAll('.subtask-item').forEach(item => {
                const text = item.querySelector('.subtask-text').textContent;
                const completed = item.querySelector('.subtask-checkbox').checked;
                subtasks.push({ text, completed });
            });
            
            if (app.isRecurringTask) {
                // Save recurring task
                const frequency = document.getElementById('recurringFrequency').value;
                const recurringTask = {
                    id: 'recurring-' + Date.now(),
                    title,
                    description,
                    priority,
                    tags: [...app.tags],
                    reminder,
                    subtasks,
                    frequency
                };
                
                app.recurringTasks.push(recurringTask);
                app.saveRecurringTasks();
                app.renderRecurringTasks();
            } else {
                // Save regular task
                const task = {
                    id: 'task-' + Date.now(),
                    title,
                    description,
                    date,
                    time,
                    duration,
                    priority,
                    tags: [...app.tags],
                    reminder,
                    subtasks,
                    status: 'pending'
                };
                
                app.tasks.push(task);
                app.saveTasks();
                
                // Render tasks for current view
                if (app.currentView === 'daily') {
                    app.renderDailyTasks();
                } else if (app.currentView === 'weekly') {
                    app.renderWeeklyTasks();
                } else if (app.currentView === 'monthly') {
                    app.renderMonthlyTasks();
                } else if (app.currentView === 'tasks') {
                    app.renderTasksList();
                }
            }
            
            app.updateStats();
            app.closeTaskModal();
        };

        app.saveTasks = function() {
            localStorage.setItem('tasks', JSON.stringify(app.tasks));
        };

        app.loadTasks = function() {
            const savedTasks = localStorage.getItem('tasks');
            if (savedTasks) {
                app.tasks = JSON.parse(savedTasks);
            }
        };

        app.saveRecurringTasks = function() {
            localStorage.setItem('recurringTasks', JSON.stringify(app.recurringTasks));
        };

        app.loadRecurringTasks = function() {
            const savedRecurringTasks = localStorage.getItem('recurringTasks');
            if (savedRecurringTasks) {
                app.recurringTasks = JSON.parse(savedRecurringTasks);
            }
        };

        app.renderDailyTasks = function() {
            const container = app.elements.tasksContainer;
            container.innerHTML = '';
            
            // Filter tasks for the current day
            const currentDateStr = app.currentDate.toISOString().split('T')[0];
            const dayTasks = app.tasks.filter(task => task.date === currentDateStr);
            
            // Create rows for tasks
            dayTasks.forEach(task => {
                const taskRow = document.createElement('div');
                taskRow.className = 'task-row';
                
                // Calculate position based on time
                const [hours, minutes] = task.time.split(':').map(Number);
                const position = ((hours - 6) * 60 + minutes) / 60 * 60; // 60px per hour
                
                // Calculate width based on duration
                const width = (task.duration / 60) * 60;
                
                // Create task element
                const taskElement = document.createElement('div');
                taskElement.className = 'task-item';
                taskElement.style.left = position + 'px';
                taskElement.style.width = width + 'px';
                taskElement.draggable = true;
                taskElement.dataset.taskId = task.id;
                
                // Set color based on priority
                if (task.priority === 'high') {
                    taskElement.style.backgroundColor = '#FEE2E2';
                    taskElement.style.borderLeft = '4px solid var(--danger)';
                } else if (task.priority === 'medium') {
                    taskElement.style.backgroundColor = '#FEF3C7';
                    taskElement.style.borderLeft = '4px solid var(--warning)';
                } else {
                    taskElement.style.backgroundColor = '#D1FAE5';
                    taskElement.style.borderLeft = '4px solid var(--secondary)';
                }
                
                // Add task content
                taskElement.innerHTML = `
                    <div class="task-header">
                        <div class="task-title">${task.title}</div>
                        <div class="task-time">${task.time} - ${app.calculateEndTime(task.time, task.duration)}</div>
                    </div>
                    <div class="task-description">${task.description || ''}</div>
                    <div class="task-footer">
                        <div class="task-tags">
                            ${task.tags.map(tag => `<span class="task-tag">${tag}</span>`).join('')}
                        </div>
                        <div class="task-priority priority-${task.priority}"></div>
                        <button class="task-delete" onclick="app.deleteTask('${task.id}')">
                            <i class="fas fa-trash"></i>
                        </button>
                    </div>
                `;
                
                // Add drag event listeners
                taskElement.addEventListener('dragstart', app.handleDragStart);
                taskElement.addEventListener('dragend', app.handleDragEnd);
                
                taskRow.appendChild(taskElement);
                container.appendChild(taskRow);
            });
            
            // Add drop event listeners to the container
            container.addEventListener('dragover', app.handleDragOver);
            container.addEventListener('drop', app.handleDrop);
        };

        app.calculateEndTime = function(startTime, durationMinutes) {
            const [hours, minutes] = startTime.split(':').map(Number);
            const totalMinutes = hours * 60 + minutes + durationMinutes;
            const endHours = Math.floor(totalMinutes / 60);
            const endMinutes = totalMinutes % 60;
            return `${endHours.toString().padStart(2, '0')}:${endMinutes.toString().padStart(2, '0')}`;
        };

        app.handleDragStart = function(e) {
            app.draggedTask = e.target;
            e.target.classList.add('dragging');
            e.dataTransfer.effectAllowed = 'move';
            e.dataTransfer.setData('text/html', e.target.innerHTML);
        };

        app.handleDragEnd = function(e) {
            e.target.classList.remove('dragging');
        };

        app.handleDragOver = function(e) {
            if (e.preventDefault) {
                e.preventDefault();
            }
            e.dataTransfer.dropEffect = 'move';
            return false;
        };

        app.handleDrop = function(e) {
            if (e.stopPropagation) {
                e.stopPropagation();
            }
            
            if (app.draggedTask) {
                const containerRect = app.elements.tasksContainer.getBoundingClientRect();
                const position = e.clientX - containerRect.left;
                
                // Calculate new time based on position
                const hourWidth = 60; // 60px per hour
                const newHour = Math.floor(position / hourWidth) + 6;
                const newMinute = Math.round(((position % hourWidth) / hourWidth) * 60);
                
                // Update task time
                const taskId = app.draggedTask.dataset.taskId;
                const task = app.tasks.find(t => t.id === taskId);
                if (task) {
                    task.time = `${newHour.toString().padStart(2, '0')}:${newMinute.toString().padStart(2, '0')}`;
                    app.saveTasks();
                    app.renderDailyTasks();
                }
            }
            
            return false;
        };

        app.deleteTask = function(taskId) {
            if (confirm('¿Estás seguro de que quieres eliminar esta tarea?')) {
                app.tasks = app.tasks.filter(task => task.id !== taskId);
                app.saveTasks();
                app.updateStats();
                
                // Re-render current view
                if (app.currentView === 'daily') {
                    app.renderDailyTasks();
                } else if (app.currentView === 'weekly') {
                    app.renderWeeklyTasks();
                } else if (app.currentView === 'monthly') {
                    app.renderMonthlyTasks();
                } else if (app.currentView === 'tasks') {
                    app.renderTasksList();
                }
            }
        };

        app.renderWeeklyTasks = function() {
            // Clear existing tasks
            document.querySelectorAll('.day-tasks').forEach(container => {
                container.innerHTML = '';
            });
            
            // Filter tasks for the current week
            const startOfWeek = new Date(app.currentDate);
            startOfWeek.setDate(app.currentDate.getDate() - app.currentDate.getDay() + 1);
            const endOfWeek = new Date(startOfWeek);
            endOfWeek.setDate(startOfWeek.getDate() + 6);
            
            const weekTasks = app.tasks.filter(task => {
                const taskDate = new Date(task.date);
                return taskDate >= startOfWeek && taskDate <= endOfWeek;
            });
            
            // Add tasks to their respective day columns
            weekTasks.forEach(task => {
                const dayColumn = document.querySelector(`.day-column[data-date="${task.date}"]`);
                if (dayColumn) {
                    const dayTasks = dayColumn.querySelector('.day-tasks');
                    
                    const taskElement = document.createElement('div');
                    taskElement.className = 'day-task';
                    
                    // Set color based on priority
                    if (task.priority === 'high') {
                        taskElement.style.backgroundColor = '#FEE2E2';
                        taskElement.style.borderLeft = '3px solid var(--danger)';
                    } else if (task.priority === 'medium') {
                        taskElement.style.backgroundColor = '#FEF3C7';
                        taskElement.style.borderLeft = '3px solid var(--warning)';
                    } else {
                        taskElement.style.backgroundColor = '#D1FAE5';
                        taskElement.style.borderLeft = '3px solid var(--secondary)';
                    }
                    
                    taskElement.innerHTML = `
                        <div>${task.time} ${task.title}</div>
                    `;
                    
                    dayTasks.appendChild(taskElement);
                }
            });
        };

        app.renderMonthlyTasks = function() {
            // Clear existing tasks
            document.querySelectorAll('.month-day-tasks').forEach(container => {
                container.innerHTML = '';
            });
            
            // Filter tasks for the current month
            const year = app.currentDate.getFullYear();
            const month = app.currentDate.getMonth();
            
            const monthTasks = app.tasks.filter(task => {
                const taskDate = new Date(task.date);
                return taskDate.getFullYear() === year && taskDate.getMonth() === month;
            });
            
            // Add tasks to their respective day columns
            monthTasks.forEach(task => {
                const dayColumn = document.querySelector(`.month-day-column[data-date="${task.date}"]`);
                if (dayColumn) {
                    const dayTasks = dayColumn.querySelector('.month-day-tasks');
                    
                    const taskElement = document.createElement('div');
                    taskElement.className = 'month-day-task';
                    taskElement.textContent = task.title;
                    taskElement.title = `${task.time} - ${task.title}`;
                    
                    // Set color based on priority
                    if (task.priority === 'high') {
                        taskElement.style.backgroundColor = 'var(--danger)';
                    } else if (task.priority === 'medium') {
                        taskElement.style.backgroundColor = 'var(--warning)';
                    } else {
                        taskElement.style.backgroundColor = 'var(--secondary)';
                    }
                    
                    dayTasks.appendChild(taskElement);
                }
            });
        };

        app.renderRecurringTasks = function() {
            const container = app.elements.recurringTasksContainer;
            container.innerHTML = '';
            
            if (app.recurringTasks.length === 0) {
                container.innerHTML = '<p style="text-align: center; color: var(--gray);">No hay tareas repetitivas</p>';
                return;
            }
            
            app.recurringTasks.forEach(task => {
                const taskElement = document.createElement('div');
                taskElement.className = 'recurring-task-item';
                
                // Set color based on priority
                if (task.priority === 'high') {
                    taskElement.style.borderLeft = '4px solid var(--danger)';
                } else if (task.priority === 'medium') {
                    taskElement.style.borderLeft = '4px solid var(--warning)';
                } else {
                    taskElement.style.borderLeft = '4px solid var(--secondary)';
                }
                
                let frequencyText = '';
                if (task.frequency === 'daily') {
                    frequencyText = 'Diaria';
                } else if (task.frequency === 'weekly') {
                    frequencyText = 'Semanal';
                } else if (task.frequency === 'monthly') {
                    frequencyText = 'Mensual';
                }
                
                taskElement.innerHTML = `
                    <div class="recurring-task-header">
                        <div class="recurring-task-title">${task.title}</div>
                        <div class="recurring-task-actions">
                            <button class="btn btn-small btn-secondary" onclick="app.deleteRecurringTask('${task.id}')">
                                <i class="fas fa-trash"></i> Eliminar
                            </button>
                        </div>
                    </div>
                    <div class="recurring-task-description">${task.description || ''}</div>
                    <div class="recurring-task-footer">
                        <div class="recurring-task-tags">
                            <span class="recurring-task-tag">${frequencyText}</span>
                            ${task.tags.map(tag => `<span class="recurring-task-tag">${tag}</span>`).join('')}
                        </div>
                        <div class="task-priority priority-${task.priority}"></div>
                    </div>
                `;
                
                container.appendChild(taskElement);
            });
        };

        app.deleteRecurringTask = function(taskId) {
            if (confirm('¿Estás seguro de que quieres eliminar esta tarea repetitiva?')) {
                app.recurringTasks = app.recurringTasks.filter(task => task.id !== taskId);
                app.saveRecurringTasks();
                app.renderRecurringTasks();
                app.updateStats();
            }
        };

        app.renderTasksList = function() {
            const container = app.elements.tasksListContainer;
            container.innerHTML = '';
            
            if (app.tasks.length === 0) {
                container.innerHTML = '<p style="text-align: center; color: var(--gray);">No hay tareas</p>';
                return;
            }
            
            // Sort tasks by date and time
            const sortedTasks = [...app.tasks].sort((a, b) => {
                const dateA = new Date(a.date + 'T' + a.time);
                const dateB = new Date(b.date + 'T' + b.time);
                return dateA - dateB;
            });
            
            sortedTasks.forEach(task => {
                const taskElement = document.createElement('div');
                taskElement.className = 'recurring-task-item';
                
                // Set color based on priority
                if (task.priority === 'high') {
                    taskElement.style.borderLeft = '4px solid var(--danger)';
                } else if (task.priority === 'medium') {
                    taskElement.style.borderLeft = '4px solid var(--warning)';
                } else {
                    taskElement.style.borderLeft = '4px solid var(--secondary)';
                }
                
                const taskDate = new Date(task.date);
                const formattedDate = taskDate.toLocaleDateString('es-ES', { 
                    weekday: 'short', 
                    year: 'numeric', 
                    month: 'short', 
                    day: 'numeric' 
                });
                
                taskElement.innerHTML = `
                    <div class="recurring-task-header">
                        <div class="recurring-task-title">${task.title}</div>
                        <div class="recurring-task-actions">
                            <button class="btn btn-small btn-secondary" onclick="app.deleteTask('${task.id}')">
                                <i class="fas fa-trash"></i> Eliminar
                            </button>
                        </div>
                    </div>
                    <div class="recurring-task-description">${task.description || ''}</div>
                    <div class="recurring-task-footer">
                        <div>
                            <div>${formattedDate} a las ${task.time}</div>
                            <div>Duración: ${task.duration} minutos</div>
                        </div>
                        <div class="task-priority priority-${task.priority}"></div>
                    </div>
                `;
                
                container.appendChild(taskElement);
            });
        };

        app.updateStats = function() {
            // Count completed tasks (tasks with all subtasks completed)
            const completedTasks = app.tasks.filter(task => {
                if (task.subtasks.length === 0) return false;
                return task.subtasks.every(subtask => subtask.completed);
            }).length;
            
            // Count pending tasks
            const pendingTasks = app.tasks.filter(task => {
                if (task.subtasks.length === 0) return true;
                return !task.subtasks.every(subtask => subtask.completed);
            }).length;
            
            // Count high priority tasks
            const highPriorityTasks = app.tasks.filter(task => task.priority === 'high').length;
            
            // Update the DOM
            document.getElementById('completedTasksCount').textContent = completedTasks;
            document.getElementById('pendingTasksCount').textContent = pendingTasks;
            document.getElementById('highPriorityTasksCount').textContent = highPriorityTasks;
        };
    </script>
</body>
</html>
