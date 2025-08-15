<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Tính Lương Trực Quan | Giao Diện Siêu Hiện Đại</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #4361ee;
            --secondary: #3a0ca3;
            --accent: #4895ef;
            --success: #4cc9f0;
            --danger: #f72585;
            --warning: #ff9e00;
            --overtime: #ff6b35;
            --glass: rgba(255, 255, 255, 0.15);
            --glass-border: rgba(255, 255, 255, 0.25);
            --glass-hover: rgba(255, 255, 255, 0.25);
            --dark: #121212;
            --light: #f8f9fa;
            --shadow: 0 10px 30px rgba(0, 0, 0, 0.25);
            --transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Poppins', sans-serif;
            -webkit-tap-highlight-color: transparent;
        }

        body {
            background: linear-gradient(135deg, #1a2a6c 0%, #3a7bd5 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 15px;
            color: white;
            position: relative;
            overflow-x: hidden;
        }

        /* Tối ưu hiệu suất */
        .bg-elements, .section::before, header::before {
            will-change: transform, opacity;
        }

        /* Background Elements */
        .bg-elements {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 1;
            overflow: hidden;
        }

        .bg-element {
            position: absolute;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.1);
            animation: float 15s infinite linear;
            filter: blur(20px);
        }

        @keyframes float {
            0% { transform: translateY(0) rotate(0deg) scale(1); }
            50% { transform: translateY(-50px) rotate(180deg) scale(1.2); }
            100% { transform: translateY(0) rotate(360deg) scale(1); }
        }

        .container {
            width: 100%;
            max-width: 1200px;
            background: rgba(18, 18, 18, 0.7);
            backdrop-filter: blur(20px);
            border-radius: 25px;
            border: 1px solid var(--glass-border);
            box-shadow: var(--shadow);
            overflow: hidden;
            animation: fadeIn 0.8s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            position: relative;
            z-index: 10;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(30px) scale(0.95); }
            to { opacity: 1; transform: translateY(0) scale(1); }
        }

        header {
            background: linear-gradient(90deg, rgba(67, 97, 238, 0.5) 0%, rgba(58, 12, 163, 0.5) 100%);
            padding: 20px 25px;
            text-align: center;
            position: relative;
            overflow: hidden;
            border-bottom: 1px solid var(--glass-border);
        }

        header::before {
            content: "";
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle, rgba(255,255,255,0.1) 0%, transparent 70%);
            transform: rotate(30deg);
            animation: shine 8s infinite linear;
            z-index: -1;
        }

        @keyframes shine {
            0% { transform: rotate(30deg) translateX(-100%); }
            100% { transform: rotate(30deg) translateX(100%); }
        }

        .header-content {
            position: relative;
            z-index: 2;
        }

        h1 {
            font-size: 1.8rem;
            margin-bottom: 8px;
            letter-spacing: 0.5px;
            text-shadow: 0 2px 10px rgba(0,0,0,0.2);
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            font-weight: 700;
            background: linear-gradient(90deg, #4cc9f0, #f72585);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .subtitle {
            font-size: 0.95rem;
            opacity: 0.85;
            max-width: 600px;
            margin: 0 auto;
            font-weight: 300;
            color: rgba(255, 255, 255, 0.8);
        }

        .language-switcher {
            position: absolute;
            top: 15px;
            right: 15px;
            display: flex;
            gap: 8px;
            z-index: 20;
        }

        .lang-btn {
            background: rgba(255, 255, 255, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.2);
            color: white;
            padding: 6px 12px;
            border-radius: 25px;
            cursor: pointer;
            transition: var(--transition);
            font-weight: 500;
            display: flex;
            align-items: center;
            gap: 6px;
            backdrop-filter: blur(5px);
            font-size: 0.9rem;
        }

        .lang-btn:hover {
            background: rgba(255, 255, 255, 0.2);
            transform: translateY(-2px);
        }

        .lang-btn.active {
            background: rgba(76, 201, 240, 0.3);
            color: white;
            box-shadow: 0 0 15px rgba(76, 201, 240, 0.3);
        }

        .content {
            display: flex;
            flex-wrap: wrap;
            padding: 20px;
            gap: 20px;
        }

        .section {
            flex: 1;
            min-width: 300px;
            background: var(--glass);
            backdrop-filter: blur(10px);
            border-radius: 22px;
            padding: 25px;
            border: 1px solid var(--glass-border);
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.2);
            position: relative;
            overflow: hidden;
            z-index: 2;
            transition: var(--transition);
        }

        .section:hover {
            transform: translateY(-8px);
            box-shadow: 0 15px 40px rgba(0, 0, 0, 0.3);
            background: rgba(255, 255, 255, 0.2);
        }

        .section::before {
            content: "";
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle, rgba(255,255,255,0.05) 0%, transparent 70%);
            transform: rotate(30deg);
            animation: shine 12s infinite linear;
            z-index: -1;
        }

        .section-title {
            display: flex;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 12px;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
            color: white;
            position: relative;
        }

        .section-title::after {
            content: "";
            position: absolute;
            bottom: -1px;
            left: 0;
            width: 50px;
            height: 3px;
            background: linear-gradient(90deg, var(--accent), var(--success));
            border-radius: 10px;
        }

        .section-title i {
            margin-right: 10px;
            font-size: 1.3rem;
            color: var(--accent);
            background: rgba(255, 255, 255, 0.1);
            width: 40px;
            height: 40px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .input-group {
            margin-bottom: 20px;
            position: relative;
        }

        .input-label {
            display: block;
            margin-bottom: 8px;
            font-weight: 500;
            color: rgba(255, 255, 255, 0.85);
            display: flex;
            align-items: center;
            gap: 8px;
            font-size: 0.95rem;
        }

        .input-label i {
            color: var(--accent);
            transition: var(--transition);
            font-size: 1.1rem;
        }

        .input-field {
            width: 100%;
            padding: 14px 14px 14px 45px;
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 14px;
            font-size: 1rem;
            transition: var(--transition);
            background: rgba(0, 0, 0, 0.2);
            color: white;
            font-weight: 500;
            backdrop-filter: blur(5px);
        }

        .input-field:focus {
            border-color: var(--accent);
            box-shadow: 0 0 0 3px rgba(67, 97, 238, 0.2);
            outline: none;
            background: rgba(0, 0, 0, 0.3);
        }

        .input-icon {
            position: absolute;
            left: 15px;
            top: 50%;
            transform: translateY(-50%);
            color: var(--accent);
            font-size: 1.1rem;
            transition: var(--transition);
        }

        .input-field:focus ~ .input-icon {
            color: var(--success);
            transform: translateY(-50%) scale(1.15);
        }

        .date-range-container {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            margin-bottom: 18px;
        }

        .date-range-item {
            flex: 1;
            min-width: 140px;
            position: relative;
        }

        .result-box {
            background: linear-gradient(135deg, rgba(58, 12, 163, 0.3) 0%, rgba(67, 97, 238, 0.3) 100%);
            border-radius: 18px;
            padding: 20px;
            margin-top: 18px;
            border-left: 4px solid var(--accent);
            animation: fadeScale 0.5s ease-out;
            backdrop-filter: blur(5px);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        @keyframes fadeScale {
            from { opacity: 0; transform: scale(0.95); }
            to { opacity: 1; transform: scale(1); }
        }

        .result-item {
            display: flex;
            justify-content: space-between;
            padding: 12px 0;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
            transition: var(--transition);
            font-size: 0.95rem;
        }

        .result-item:hover {
            background: rgba(255,255,255,0.05);
            transform: translateX(4px);
        }

        .result-item:last-child {
            border-bottom: none;
        }

        .result-label {
            font-weight: 500;
            color: rgba(255, 255, 255, 0.9);
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .result-label i {
            color: var(--accent);
            font-size: 1.1rem;
        }

        .result-value {
            font-weight: 600;
            color: white;
            transition: var(--transition);
            font-size: 1rem;
        }

        .total {
            font-size: 1.2rem;
            color: white;
            margin-top: 12px;
            padding-top: 12px;
            border-top: 2px solid var(--accent);
        }

        .total-value {
            font-size: 1.4rem;
            color: var(--success);
            text-shadow: 0 0 10px rgba(76, 201, 240, 0.5);
            transition: var(--transition);
            background: linear-gradient(90deg, #ff9e00, #ff6b35);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .calculate-btn {
            display: block;
            width: 100%;
            padding: 16px;
            background: linear-gradient(90deg, var(--primary) 0%, var(--secondary) 100%);
            color: white;
            border: none;
            border-radius: 14px;
            font-size: 1.1rem;
            font-weight: 600;
            cursor: pointer;
            transition: var(--transition);
            margin-top: 18px;
            box-shadow: 0 8px 20px rgba(67, 97, 238, 0.3);
            position: relative;
            overflow: hidden;
            z-index: 1;
            backdrop-filter: blur(5px);
            border: 1px solid rgba(255, 255, 255, 0.2);
        }

        .calculate-btn::before {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, var(--secondary) 0%, var(--primary) 100%);
            z-index: -1;
            opacity: 0;
            transition: var(--transition);
        }

        .calculate-btn:hover {
            transform: translateY(-4px);
            box-shadow: 0 12px 25px rgba(67, 97, 238, 0.4);
        }

        .calculate-btn:hover::before {
            opacity: 1;
        }

        .calculate-btn:active {
            transform: translateY(-2px);
        }

        .bonus-info {
            background: rgba(76, 201, 240, 0.15);
            padding: 12px;
            border-radius: 14px;
            margin-top: 18px;
            font-size: 0.9rem;
            color: rgba(255, 255, 255, 0.9);
            border-left: 4px solid var(--success);
            animation: fadeIn 0.6s ease-out;
            backdrop-filter: blur(5px);
        }

        .bonus-info i {
            color: var(--success);
            margin-right: 8px;
        }

        footer {
            text-align: center;
            padding: 15px;
            color: rgba(255, 255, 255, 0.7);
            background: rgba(0, 0, 0, 0.2);
            font-size: 0.85rem;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(5px);
        }

        .working-days-display {
            background: linear-gradient(90deg, rgba(67, 97, 238, 0.3) 0%, rgba(58, 12, 163, 0.3) 100%);
            color: white;
            padding: 14px;
            border-radius: 14px;
            text-align: center;
            margin-bottom: 18px;
            font-size: 1.1rem;
            position: relative;
            overflow: hidden;
            animation: pulse 2s infinite;
            border: 1px solid rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(5px);
        }

        @keyframes pulse {
            0% { box-shadow: 0 0 0 0 rgba(67, 97, 238, 0.4); }
            70% { box-shadow: 0 0 0 12px rgba(67, 97, 238, 0); }
            100% { box-shadow: 0 0 0 0 rgba(67, 97, 238, 0); }
        }

        .calendar-container {
            background: rgba(0, 0, 0, 0.2);
            border-radius: 18px;
            padding: 18px;
            margin-top: 18px;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
            animation: fadeIn 0.8s ease-out;
            border: 1px solid rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(5px);
        }

        .calendar-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 12px;
        }

        .calendar-nav {
            display: flex;
            gap: 8px;
        }

        .nav-btn {
            width: 36px;
            height: 36px;
            border-radius: 50%;
            background: rgba(67, 97, 238, 0.3);
            color: white;
            border: none;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: var(--transition);
            box-shadow: 0 4px 8px rgba(0,0,0,0.2);
            backdrop-filter: blur(5px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            font-size: 0.9rem;
        }

        .nav-btn:hover {
            transform: scale(1.08);
            background: rgba(76, 201, 240, 0.4);
        }

        .current-month {
            font-weight: 600;
            color: white;
            font-size: 1rem;
        }

        .calendar-grid {
            display: grid;
            grid-template-columns: repeat(7, 1fr);
            gap: 6px;
        }

        .calendar-day {
            text-align: center;
            padding: 10px 0;
            font-weight: 600;
            color: rgba(255, 255, 255, 0.7);
            font-size: 0.85rem;
        }

        .calendar-cell {
            height: 38px;
            display: flex;
            justify-content: center;
            align-items: center;
            border-radius: 10px;
            cursor: pointer;
            transition: var(--transition);
            font-weight: 500;
            position: relative;
            background: rgba(0, 0, 0, 0.2);
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
            backdrop-filter: blur(5px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            color: white;
            font-size: 0.9rem;
        }

        .calendar-cell:hover {
            background: rgba(67, 97, 238, 0.3);
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(67, 97, 238, 0.2);
        }

        .sunday {
            color: var(--danger);
            background: rgba(247, 37, 133, 0.15);
        }

        .sunday:hover {
            background: rgba(247, 37, 133, 0.25);
        }

        .selected {
            background: var(--primary) !important;
            color: white !important;
            box-shadow: 0 5px 15px rgba(67, 97, 238, 0.4);
            transform: scale(1.05);
            animation: pulse 1.5s infinite;
        }

        .off-day-selected {
            background: var(--danger) !important;
            color: white !important;
            position: relative;
        }

        .off-day-selected::after {
            content: "Nghỉ";
            position: absolute;
            bottom: 2px;
            right: 2px;
            font-size: 0.5rem;
            background: white;
            color: var(--danger);
            border-radius: 3px;
            padding: 0 3px;
        }
        
        .off-day-indicator {
            position: absolute;
            top: 2px;
            right: 2px;
            width: 5px;
            height: 5px;
            border-radius: 50%;
            background: var(--danger);
        }

        .other-month {
            color: rgba(255, 255, 255, 0.3);
            background: rgba(0, 0, 0, 0.1);
        }

        /* Cải tiến phần chọn ngày nghỉ */
        .off-day-controls {
            background: rgba(247, 37, 133, 0.15);
            border-radius: 14px;
            padding: 18px;
            margin-top: 18px;
            border: 1px dashed rgba(247, 37, 133, 0.3);
            animation: fadeIn 0.5s ease-out;
            backdrop-filter: blur(5px);
        }

        .off-day-header {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-bottom: 14px;
        }

        .off-day-title {
            display: flex;
            align-items: center;
            font-weight: 600;
            color: rgba(255, 255, 255, 0.9);
            gap: 8px;
            font-size: 1rem;
        }

        .off-day-counter {
            background: var(--danger);
            color: white;
            padding: 4px 10px;
            border-radius: 18px;
            font-size: 0.85rem;
            backdrop-filter: blur(5px);
        }

        .off-days-list {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
            min-height: 36px;
        }

        .off-day-item {
            background: rgba(247, 37, 133, 0.2);
            padding: 8px 12px;
            border-radius: 18px;
            display: inline-flex;
            align-items: center;
            font-size: 0.85rem;
            position: relative;
            transition: var(--transition);
            animation: popIn 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            backdrop-filter: blur(5px);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        @keyframes popIn {
            from { opacity: 0; transform: scale(0.8); }
            to { opacity: 1; transform: scale(1); }
        }

        @keyframes fadeOut {
            from { opacity: 1; transform: scale(1); }
            to { opacity: 0; transform: scale(0); }
        }

        .off-day-item:hover {
            transform: translateY(-3px);
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
            background: rgba(247, 37, 133, 0.3);
        }

        .off-day-item i {
            margin-right: 5px;
            color: white;
            cursor: pointer;
            transition: var(--transition);
            font-size: 0.9rem;
        }

        .off-day-item i:hover {
            transform: scale(1.2);
            color: var(--warning);
        }

        .off-day-type {
            background: rgba(255, 255, 255, 0.2);
            color: white;
            padding: 3px 8px;
            border-radius: 18px;
            font-size: 0.75rem;
            margin-left: 6px;
            backdrop-filter: blur(5px);
        }

        .add-off-day {
            display: flex;
            margin-top: 14px;
            flex-wrap: wrap;
            gap: 8px;
        }

        .add-off-day input, .add-off-day select {
            flex: 1;
            min-width: 110px;
            padding: 10px;
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 10px;
            background: rgba(0, 0, 0, 0.2);
            transition: var(--transition);
            color: white;
            backdrop-filter: blur(5px);
            font-size: 0.9rem;
        }

        .add-off-day input:focus, .add-off-day select:focus {
            border-color: var(--danger);
            box-shadow: 0 0 0 3px rgba(247, 37, 133, 0.2);
            outline: none;
        }

        .add-off-day button {
            background: var(--danger);
            color: white;
            border: none;
            padding: 0 16px;
            border-radius: 10px;
            cursor: pointer;
            transition: var(--transition);
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 4px 10px rgba(247, 37, 133, 0.3);
            gap: 6px;
            font-weight: 500;
            backdrop-filter: blur(5px);
            border: 1px solid rgba(255, 255, 255, 0.2);
            font-size: 0.9rem;
        }

        .add-off-day button:hover {
            background: #e91e63;
            transform: translateY(-3px);
            box-shadow: 0 6px 15px rgba(247, 37, 133, 0.4);
        }

        .no-off-days {
            width: 100%;
            text-align: center;
            padding: 8px;
            color: rgba(255, 255, 255, 0.5);
            font-style: italic;
            font-size: 0.9rem;
        }

        /* Overtime Styles */
        .overtime-section {
            background: rgba(255, 158, 0, 0.15);
            border-radius: 14px;
            padding: 18px;
            margin-top: 18px;
            border: 1px dashed rgba(255, 158, 0, 0.3);
            animation: fadeIn 0.5s ease-out;
            backdrop-filter: blur(5px);
        }

        .overtime-header {
            display: flex;
            align-items: center;
            margin-bottom: 14px;
        }

        .overtime-title {
            display: flex;
            align-items: center;
            font-weight: 600;
            color: rgba(255, 255, 255, 0.9);
            gap: 8px;
            font-size: 1rem;
        }

        /* Chatbot Styles */
        .chatbot-container {
            position: fixed;
            bottom: 20px;
            right: 20px;
            z-index: 1000;
            transition: var(--transition);
        }

        .chatbot-toggle {
            width: 55px;
            height: 55px;
            border-radius: 50%;
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            color: white;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            box-shadow: 0 8px 20px rgba(0,0,0,0.3);
            transition: var(--transition);
            font-size: 1.6rem;
            position: relative;
            border: 1px solid rgba(255, 255, 255, 0.2);
            backdrop-filter: blur(5px);
        }

        .chatbot-toggle:hover {
            transform: scale(1.08) rotate(15deg);
            box-shadow: 0 12px 25px rgba(67, 97, 238, 0.4);
        }

        .chatbot-toggle .notification {
            position: absolute;
            top: -5px;
            right: -5px;
            background: var(--danger);
            color: white;
            width: 22px;
            height: 22px;
            border-radius: 50%;
            font-size: 0.75rem;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 2px 5px rgba(0,0,0,0.2);
        }

        .chatbot-window {
            position: absolute;
            bottom: 65px;
            right: 0;
            width: 320px;
            height: 400px;
            background: rgba(18, 18, 18, 0.8);
            border-radius: 22px;
            box-shadow: 0 12px 35px rgba(0,0,0,0.3);
            display: flex;
            flex-direction: column;
            overflow: hidden;
            transform: translateY(20px);
            opacity: 0;
            pointer-events: none;
            transition: var(--transition);
            border: 1px solid rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(20px);
        }

        .chatbot-window.active {
            transform: translateY(0);
            opacity: 1;
            pointer-events: all;
        }

        .chatbot-header {
            background: linear-gradient(90deg, rgba(67, 97, 238, 0.5) 0%, rgba(58, 12, 163, 0.5) 100%);
            color: white;
            padding: 16px;
            display: flex;
            align-items: center;
            gap: 12px;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
        }

        .chatbot-header h3 {
            font-weight: 500;
            font-size: 1.15rem;
        }

        .chatbot-messages {
            flex-grow: 1;
            padding: 16px;
            overflow-y: auto;
            display: flex;
            flex-direction: column;
            gap: 12px;
            background: rgba(0, 0, 0, 0.2);
        }

        .message {
            max-width: 85%;
            padding: 12px 16px;
            border-radius: 18px;
            font-size: 0.95rem;
            animation: fadeIn 0.3s ease;
            backdrop-filter: blur(5px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            line-height: 1.5;
        }

        .message.bot {
            background: rgba(58, 12, 163, 0.2);
            align-self: flex-start;
            border-bottom-left-radius: 5px;
            color: rgba(255, 255, 255, 0.9);
        }

        .message.user {
            background: rgba(67, 97, 238, 0.3);
            color: white;
            align-self: flex-end;
            border-bottom-right-radius: 5px;
        }

        .chatbot-input {
            padding: 16px;
            display: flex;
            gap: 12px;
            background: rgba(0, 0, 0, 0.3);
            border-top: 1px solid rgba(255, 255, 255, 0.1);
        }

        .chatbot-input input {
            flex-grow: 1;
            padding: 12px 16px;
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 25px;
            outline: none;
            transition: var(--transition);
            background: rgba(0, 0, 0, 0.2);
            color: white;
            font-size: 0.95rem;
            backdrop-filter: blur(5px);
        }

        .chatbot-input input:focus {
            border-color: var(--primary);
            box-shadow: 0 0 0 3px rgba(67, 97, 238, 0.2);
        }

        .chatbot-input button {
            width: 45px;
            height: 45px;
            border-radius: 50%;
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            color: white;
            border: none;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: var(--transition);
            font-size: 1.1rem;
            box-shadow: 0 4px 12px rgba(0,0,0,0.2);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        .chatbot-input button:hover {
            transform: rotate(15deg) scale(1.08);
            box-shadow: 0 6px 16px rgba(67, 97, 238, 0.4);
        }

        .quick-questions {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
            margin-top: 12px;
        }

        .quick-question {
            background: rgba(67, 97, 238, 0.3);
            color: white;
            border: none;
            padding: 8px 12px;
            border-radius: 22px;
            font-size: 0.85rem;
            cursor: pointer;
            transition: var(--transition);
            border: 1px solid rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(5px);
        }

        .quick-question:hover {
            background: rgba(76, 201, 240, 0.4);
            transform: translateY(-2px);
        }

        /* Media queries for mobile optimization */
        @media (max-width: 768px) {
            .content {
                flex-direction: column;
                padding: 15px;
                gap: 15px;
            }
            
            h1 {
                font-size: 1.6rem;
                gap: 8px;
            }
            
            .section {
                padding: 20px;
                border-radius: 20px;
            }
            
            .section-title {
                margin-bottom: 18px;
                font-size: 1.1rem;
            }
            
            .section-title i {
                width: 36px;
                height: 36px;
                font-size: 1.1rem;
            }
            
            .date-range-container {
                gap: 10px;
            }
            
            .date-range-item {
                min-width: 100%;
            }
            
            .input-field {
                padding: 12px 12px 12px 40px;
                font-size: 0.95rem;
            }
            
            .input-icon {
                font-size: 1rem;
            }
            
            .working-days-display {
                padding: 12px;
                font-size: 1rem;
            }
            
            .calendar-container {
                padding: 15px;
            }
            
            .calendar-cell {
                height: 34px;
                font-size: 0.85rem;
            }
            
            .result-item {
                font-size: 0.9rem;
            }
            
            .total-value {
                font-size: 1.3rem;
            }
            
            .calculate-btn {
                padding: 14px;
                font-size: 1rem;
            }
            
            .chatbot-window {
                width: 300px;
                height: 380px;
                bottom: 60px;
            }
            
            .language-switcher {
                top: 10px;
                right: 10px;
            }
            
            header {
                padding: 15px 20px;
            }
            
            .off-day-controls {
                padding: 15px;
            }
            
            .add-off-day button {
                padding: 0 14px;
            }
        }

        @media (max-width: 480px) {
            h1 {
                font-size: 1.4rem;
                flex-direction: column;
                gap: 5px;
            }
            
            .section {
                padding: 18px;
                border-radius: 18px;
            }
            
            .section-title {
                font-size: 1rem;
            }
            
            .input-label {
                font-size: 0.9rem;
            }
            
            .input-field {
                font-size: 0.9rem;
            }
            
            .calendar-cell {
                height: 30px;
                font-size: 0.8rem;
            }
            
            .calendar-day {
                font-size: 0.8rem;
            }
            
            .result-item {
                font-size: 0.85rem;
            }
            
            .total {
                font-size: 1.1rem;
            }
            
            .total-value {
                font-size: 1.2rem;
            }
            
            .chatbot-toggle {
                width: 50px;
                height: 50px;
                font-size: 1.5rem;
            }
            
            .chatbot-window {
                width: 280px;
                height: 360px;
            }
            
            .message {
                font-size: 0.9rem;
            }
            
            .chatbot-input input {
                padding: 10px 14px;
            }
            
            .chatbot-input button {
                width: 40px;
                height: 40px;
            }
            
            .quick-question {
                font-size: 0.8rem;
                padding: 6px 10px;
            }
        }
    </style>
</head>
<body>
    <!-- Background decorative elements -->
    <div class="bg-elements">
        <div class="bg-element" style="width: 300px; height: 300px; top: 10%; left: 5%; animation-duration: 20s; background: rgba(67, 97, 238, 0.1);"></div>
        <div class="bg-element" style="width: 200px; height: 200px; top: 70%; left: 80%; animation-duration: 15s; background: rgba(247, 37, 133, 0.1);"></div>
        <div class="bg-element" style="width: 250px; height: 250px; top: 30%; left: 85%; animation-duration: 25s; background: rgba(76, 201, 240, 0.1);"></div>
        <div class="bg-element" style="width: 350px; height: 350px; top: 80%; left: 10%; animation-duration: 18s; background: rgba(255, 158, 0, 0.1);"></div>
        <div class="bg-element" style="width: 180px; height: 180px; top: 20%; left: 70%; animation-duration: 22s; background: rgba(58, 12, 163, 0.1);"></div>
    </div>

    <div class="container">
        <header>
            <div class="language-switcher">
                <button class="lang-btn active" id="lang-vi">
                    <i class="fas fa-language"></i> VI
                </button>
                <button class="lang-btn" id="lang-en">
                    <i class="fas fa-language"></i> EN
                </button>
            </div>
            
            <div class="header-content">
                <h1>
                    <i class="fas fa-calculator"></i>
                    <span id="app-title">TÍNH LƯƠNG TRỰC QUAN</span>
                </h1>
                <p class="subtitle" id="app-subtitle">Giao diện siêu hiện đại với hiệu ứng chuyển động mượt mà</p>
            </div>
        </header>
        
        <div class="content">
            <div class="section">
                <div class="section-title">
                    <i class="far fa-calendar-alt"></i>
                    <h2 id="time-period-title">Chọn khoảng thời gian</h2>
                </div>
                
                <div class="date-range-container">
                    <div class="date-range-item">
                        <label class="input-label" for="start-date">
                            <i class="fas fa-calendar-day"></i> <span id="from-date-label">Từ ngày</span>
                        </label>
                        <div class="input-icon">
                            <i class="fas fa-calendar"></i>
                        </div>
                        <input type="date" id="start-date" class="input-field">
                    </div>
                    
                    <div class="date-range-item">
                        <label class="input-label" for="end-date">
                            <i class="fas fa-calendar-week"></i> <span id="to-date-label">Đến ngày</span>
                        </label>
                        <div class="input-icon">
                            <i class="fas fa-calendar"></i>
                        </div>
                        <input type="date" id="end-date" class="input-field">
                    </div>
                </div>
                
                <div class="working-days-display">
                    <i class="fas fa-calendar-check"></i> <span id="working-days-label">Ngày công:</span> <span id="working-days-count">0</span> <span id="days-label">ngày</span>
                </div>
                
                <div class="calendar-container">
                    <div class="calendar-header">
                        <div class="calendar-nav">
                            <button class="nav-btn" id="prev-month"><i class="fas fa-chevron-left"></i></button>
                            <button class="nav-btn" id="next-month"><i class="fas fa-chevron-right"></i></button>
                        </div>
                        <div class="current-month" id="current-month">Tháng 8, 2025</div>
                    </div>
                    
                    <div class="calendar-grid">
                        <div class="calendar-day">T2</div>
                        <div class="calendar-day">T3</div>
                        <div class="calendar-day">T4</div>
                        <div class="calendar-day">T5</div>
                        <div class="calendar-day">T6</div>
                        <div class="calendar-day">T7</div>
                        <div class="calendar-day">CN</div>
                        
                        <!-- Calendar cells will be generated by JavaScript -->
                    </div>
                </div>
                
                <div class="input-group">
                    <label class="input-label" for="daily-salary">
                        <i class="fas fa-coins"></i> <span id="daily-salary-label">Lương ngày (VNĐ)</span>
                    </label>
                    <div class="input-icon">
                        <i class="fas fa-money-bill-wave"></i>
                    </div>
                    <input type="number" id="daily-salary" class="input-field" placeholder="Nhập lương một ngày làm việc" min="0" value="350000">
                </div>
            </div>
            
            <div class="section">
                <div class="section-title">
                    <i class="fas fa-money-bill-wave"></i>
                    <h2 id="bonus-title">Thưởng & Ngày nghỉ</h2>
                </div>
                
                <div class="input-group">
                    <label class="input-label" for="attendance-bonus">
                        <i class="fas fa-award"></i> <span id="attendance-bonus-label">Tiền chuyên cần (VNĐ)</span>
                    </label>
                    <div class="input-icon">
                        <i class="fas fa-trophy"></i>
                    </div>
                    <input type="number" id="attendance-bonus" class="input-field" placeholder="Nhập tiền thưởng chuyên cần" min="0" value="500000">
                    <div class="bonus-info">
                        <i class="fas fa-info-circle"></i> <span id="bonus-info-text">Tiền chuyên cần chỉ được tính khi đủ 24 ngày công</span>
                    </div>
                </div>
                
                <div class="input-group">
                    <label class="input-label" for="special-bonus">
                        <i class="fas fa-star"></i> <span id="special-bonus-label">Tiền công đoạn đặc biệt (VNĐ)</span>
                    </label>
                    <div class="input-icon">
                        <i class="fas fa-gem"></i>
                    </div>
                    <input type="number" id="special-bonus" class="input-field" placeholder="Nhập tiền công đoạn đặc biệt" min="0" value="0">
                </div>
                
                <!-- Phần tăng ca mới -->
                <div class="overtime-section">
                    <div class="overtime-header">
                        <div class="overtime-title">
                            <i class="fas fa-clock"></i>
                            <span id="overtime-title">Tính lương tăng ca</span>
                        </div>
                    </div>
                    
                    <div class="input-group">
                        <label class="input-label" for="overtime-hours">
                            <i class="fas fa-business-time"></i> <span id="overtime-hours-label">Số giờ tăng ca</span>
                        </label>
                        <div class="input-icon">
                            <i class="fas fa-hourglass-half"></i>
                        </div>
                        <input type="number" id="overtime-hours" class="input-field" placeholder="Nhập số giờ tăng ca" min="0" value="0">
                    </div>
                    
                    <div class="input-group">
                        <label class="input-label" for="overtime-rate">
                            <i class="fas fa-money-bill-wave"></i> <span id="overtime-rate-label">Lương tăng ca/giờ (VNĐ)</span>
                        </label>
                        <div class="input-icon">
                            <i class="fas fa-coins"></i>
                        </div>
                        <input type="number" id="overtime-rate" class="input-field" placeholder="Nhập lương tăng ca mỗi giờ" min="0" value="50000">
                    </div>
                </div>
                
                <!-- Cải tiến phần chọn ngày nghỉ -->
                <div class="off-day-controls">
                    <div class="off-day-header">
                        <div class="off-day-title">
                            <i class="fas fa-calendar-times"></i>
                            <span id="off-day-title">Quản lý ngày nghỉ</span>
                        </div>
                        <div class="off-day-counter">
                            <span id="off-day-count">0</span> <span id="off-day-label">ngày nghỉ</span>
                        </div>
                    </div>
                    
                    <div class="off-days-list" id="off-days-list">
                        <div class="no-off-days" id="no-off-days">Chưa có ngày nghỉ nào được thêm</div>
                    </div>
                    
                    <div class="add-off-day">
                        <input type="date" id="new-off-day" class="input-field">
                        <select id="off-day-type" class="input-field">
                            <option value="full">Nghỉ cả ngày (0%)</option>
                            <option value="half">Nghỉ nửa ngày (50%)</option>
                            <option value="quarter">Nghỉ 1/4 ngày (70%)</option>
                            <option value="three_quarter">Nghỉ 3/4 ngày (30%)</option>
                        </select>
                        <button id="add-off-day-btn"><i class="fas fa-plus"></i> <span id="add-off-day-label">Thêm</span></button>
                    </div>
                </div>
                
                <div class="result-box">
                    <div class="result-item">
                        <span class="result-label"><i class="fas fa-calculator"></i> <span id="basic-salary-label">Lương cơ bản:</span></span>
                        <span class="result-value" id="basic-salary">0 VNĐ</span>
                    </div>
                    <div class="result-item">
                        <span class="result-label"><i class="fas fa-trophy"></i> <span id="attendance-result-label">Tiền chuyên cần:</span></span>
                        <span class="result-value" id="attendance-result">0 VNĐ</span>
                    </div>
                    <div class="result-item">
                        <span class="result-label"><i class="fas fa-gem"></i> <span id="special-result-label">Công đoạn đặc biệt:</span></span>
                        <span class="result-value" id="special-result">0 VNĐ</span>
                    </div>
                    <!-- Dòng mới cho tiền tăng ca -->
                    <div class="result-item">
                        <span class="result-label"><i class="fas fa-clock"></i> <span id="overtime-result-label">Tiền tăng ca:</span></span>
                        <span class="result-value" id="overtime-result">0 VNĐ</span>
                    </div>
                    <div class="result-item total">
                        <span class="result-label"><i class="fas fa-wallet"></i> <span id="total-salary-label">TỔNG LƯƠNG:</span></span>
                        <span class="result-value total-value" id="total-salary">0 VNĐ</span>
                    </div>
                </div>
                
                <button class="calculate-btn" id="calculate-btn">
                    <i class="fas fa-calculator"></i> <span id="calculate-btn-label">TÍNH LƯƠNG</span>
                </button>
            </div>
        </div>
        
        <footer>
            <p id="footer-text">© 2023 Ứng dụng Tính Lương Nâng Cao | Giao diện siêu hiện đại với hiệu ứng chuyển động mượt mà</p>
        </footer>
    </div>

    <!-- Chatbot -->
    <div class="chatbot-container">
        <div class="chatbot-toggle" id="chatbot-toggle">
            <i class="fas fa-robot"></i>
            <div class="notification">1</div>
        </div>
        <div class="chatbot-window" id="chatbot-window">
            <div class="chatbot-header">
                <i class="fas fa-robot"></i>
                <h3 id="chatbot-title">Trợ lý tính lương</h3>
            </div>
            <div class="chatbot-messages" id="chatbot-messages">
                <div class="message bot" id="welcome-message">
                    Xin chào! Tôi có thể giúp gì cho bạn về tính lương? Dưới đây là một số câu hỏi thường gặp:
                    <div class="quick-questions">
                        <button class="quick-question" data-question="how-to-use">Cách sử dụng ứng dụng</button>
                        <button class="quick-question" data-question="bonus-calculation">Cách tính tiền thưởng</button>
                        <button class="quick-question" data-question="overtime">Cách tính lương tăng ca</button>
                        <button class="quick-question" data-question="day-off">Cách thêm ngày nghỉ</button>
                    </div>
                </div>
            </div>
            <div class="chatbot-input">
                <input type="text" id="chat-input" placeholder="Nhập câu hỏi của bạn...">
                <button id="send-message"><i class="fas fa-paper-plane"></i></button>
            </div>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // Khởi tạo dữ liệu
            const today = new Date(2025, 7, 1); // Tháng 8, 2025
            const firstDayOfMonth = new Date(today.getFullYear(), today.getMonth(), 1);
            const lastDayOfMonth = new Date(today.getFullYear(), today.getMonth() + 1, 0);
            
            let currentDate = new Date(2025, 7, 1); // Tháng 8, 2025
            let currentMonth = currentDate.getMonth();
            let currentYear = currentDate.getFullYear();
            
            // Biến lưu trữ ngày nghỉ
            let offDays = [];
            
            // Định dạng ngày thành chuỗi YYYY-MM-DD
            function formatDate(date) {
                const year = date.getFullYear();
                const month = String(date.getMonth() + 1).padStart(2, '0');
                const day = String(date.getDate()).padStart(2, '0');
                return `${year}-${month}-${day}`;
            }
            
            // Đặt giá trị mặc định cho input ngày
            document.getElementById('start-date').value = formatDate(firstDayOfMonth);
            document.getElementById('end-date').value = formatDate(lastDayOfMonth);
            
            // Hàm tính số ngày công (không tính chủ nhật và ngày nghỉ)
            function calculateWorkingDays() {
                const startDate = new Date(document.getElementById('start-date').value);
                const endDate = new Date(document.getElementById('end-date').value);
                
                if (!startDate || !endDate || startDate > endDate) {
                    return {
                        fullDays: 0,
                        halfDays: 0,
                        quarterDays: 0,
                        threeQuarterDays: 0,
                        totalDays: 0
                    };
                }
                
                // Biến đếm các loại ngày
                let fullDays = 0;
                let halfDays = 0;
                let quarterDays = 0;
                let threeQuarterDays = 0;
                let totalDays = 0;
                
                let currentDate = new Date(startDate);
                
                while (currentDate <= endDate) {
                    // Chủ nhật là ngày 0
                    if (currentDate.getDay() !== 0) {
                        const dateStr = formatDate(currentDate);
                        const offDay = offDays.find(day => day.date === dateStr);
                        
                        if (!offDay) {
                            // Ngày làm việc đầy đủ
                            fullDays++;
                            totalDays += 1;
                        } else {
                            // Xử lý các loại nghỉ
                            switch(offDay.type) {
                                case 'half':
                                    halfDays++;
                                    totalDays += 0.5;
                                    break;
                                case 'quarter':
                                    quarterDays++;
                                    totalDays += 0.7;
                                    break;
                                case 'three_quarter':
                                    threeQuarterDays++;
                                    totalDays += 0.3;
                                    break;
                                // Nghỉ cả ngày không cộng gì
                            }
                        }
                    }
                    currentDate.setDate(currentDate.getDate() + 1);
                }
                
                return {
                    fullDays,
                    halfDays,
                    quarterDays,
                    threeQuarterDays,
                    totalDays
                };
            }
            
            // Hàm cập nhật lịch
            function updateCalendar() {
                const calendarGrid = document.querySelector('.calendar-grid');
                const monthYearElement = document.getElementById('current-month');
                
                // Xóa lịch cũ (giữ lại các ngày trong tuần)
                while (calendarGrid.children.length > 7) {
                    calendarGrid.removeChild(calendarGrid.lastChild);
                }
                
                // Lấy ngày đầu tiên và ngày cuối cùng của tháng
                const firstDay = new Date(currentYear, currentMonth, 1);
                const lastDay = new Date(currentYear, currentMonth + 1, 0);
                
                // Tính toán ngày trong tuần của ngày đầu tiên
                const firstDayOfWeek = firstDay.getDay();
                const adjustedFirstDayOfWeek = (firstDayOfWeek + 6) % 7; // 0 = Thứ 2, 6 = Chủ nhật
                
                // Cập nhật hiển thị tháng/năm
                const monthNames = ["Tháng 1", "Tháng 2", "Tháng 3", "Tháng 4", "Tháng 5", "Tháng 6",
                                   "Tháng 7", "Tháng 8", "Tháng 9", "Tháng 10", "Tháng 11", "Tháng 12"];
                monthYearElement.textContent = `${monthNames[currentMonth]}, ${currentYear}`;
                
                // Tạo các ô trống cho những ngày trước ngày đầu tiên của tháng
                for (let i = 0; i < adjustedFirstDayOfWeek; i++) {
                    const cell = document.createElement('div');
                    cell.className = 'calendar-cell other-month';
                    calendarGrid.appendChild(cell);
                }
                
                // Tạo các ô cho tất cả các ngày trong tháng
                for (let day = 1; day <= lastDay.getDate(); day++) {
                    const cell = document.createElement('div');
                    cell.className = 'calendar-cell';
                    cell.textContent = day;
                    
                    // Tính toán ngày trong tuần
                    const cellDate = new Date(currentYear, currentMonth, day);
                    const dayOfWeek = (cellDate.getDay() + 6) % 7;
                    const dateStr = formatDate(cellDate);
                    
                    // Đánh dấu Chủ nhật
                    if (dayOfWeek === 6) {
                        cell.classList.add('sunday');
                    }
                    
                    // Kiểm tra nếu là ngày nghỉ
                    const offDay = offDays.find(d => d.date === dateStr);
                    if (offDay) {
                        cell.classList.add('off-day-selected');
                        
                        // Thêm chỉ báo ngày nghỉ
                        const indicator = document.createElement('div');
                        indicator.className = 'off-day-indicator';
                        cell.appendChild(indicator);
                    }
                    
                    // Thêm sự kiện click cho ô lịch
                    cell.addEventListener('click', function() {
                        // Chỉ xử lý nếu không phải chủ nhật
                        if (dayOfWeek !== 6) {
                            toggleOffDay(dateStr);
                        }
                    });
                    
                    calendarGrid.appendChild(cell);
                }
            }
            
            // Cập nhật hiển thị ngày nghỉ
            function updateOffDaysDisplay() {
                const offDaysList = document.getElementById('off-days-list');
                const offDayCount = document.getElementById('off-day-count');
                offDaysList.innerHTML = '';
                
                offDayCount.textContent = offDays.length;
                
                if (offDays.length === 0) {
                    offDaysList.innerHTML = '<div class="no-off-days" id="no-off-days">Chưa có ngày nghỉ nào được thêm</div>';
                    return;
                }
                
                offDays.forEach(day => {
                    const date = new Date(day.date);
                    const formattedDate = date.toLocaleDateString('vi-VN', {
                        day: '2-digit',
                        month: '2-digit',
                        year: 'numeric'
                    });
                    
                    let typeText = '';
                    let typeClass = '';
                    
                    switch(day.type) {
                        case 'full':
                            typeText = 'Nghỉ cả ngày';
                            typeClass = 'off-day-type';
                            break;
                        case 'half':
                            typeText = 'Nghỉ nửa ngày';
                            typeClass = 'off-day-type half';
                            break;
                        case 'quarter':
                            typeText = 'Nghỉ 1/4 ngày';
                            typeClass = 'off-day-type quarter';
                            break;
                        case 'three_quarter':
                            typeText = 'Nghỉ 3/4 ngày';
                            typeClass = 'off-day-type three-quarter';
                            break;
                    }
                    
                    const offDayElement = document.createElement('div');
                    offDayElement.className = 'off-day-item';
                    offDayElement.innerHTML = `
                        <i class="fas fa-times remove-off-day" data-date="${day.date}"></i>
                        ${formattedDate}
                        <span class="${typeClass}">${typeText}</span>
                    `;
                    offDaysList.appendChild(offDayElement);
                });
                
                // Thêm sự kiện xóa ngày nghỉ
                document.querySelectorAll('.remove-off-day').forEach(btn => {
                    btn.addEventListener('click', function() {
                        const offDayElement = this.parentElement;
                        offDayElement.style.animation = "fadeOut 0.3s forwards";
                        
                        setTimeout(() => {
                            const dateToRemove = this.getAttribute('data-date');
                            offDays = offDays.filter(day => day.date !== dateToRemove);
                            updateOffDaysDisplay();
                            updateCalendar();
                            calculateSalary();
                        }, 300);
                    });
                });
            }
            
            // Hàm thêm/xóa ngày nghỉ
            function toggleOffDay(dateStr) {
                // Tìm xem ngày này đã có trong offDays chưa
                const existingIndex = offDays.findIndex(day => day.date === dateStr);
                
                if (existingIndex !== -1) {
                    // Nếu có, xóa đi
                    offDays.splice(existingIndex, 1);
                } else {
                    // Nếu chưa, thêm vào với loại mặc định là 'full'
                    offDays.push({
                        date: dateStr,
                        type: 'full'
                    });
                }
                
                updateCalendar();
                updateOffDaysDisplay();
                calculateSalary();
            }
            
            // Hàm tính lương (bao gồm cả tăng ca)
            function calculateSalary() {
                const days = calculateWorkingDays();
                document.getElementById('working-days-count').textContent = days.totalDays.toFixed(1);
                
                const dailySalary = parseFloat(document.getElementById('daily-salary').value) || 0;
                const attendanceBonus = parseFloat(document.getElementById('attendance-bonus').value) || 0;
                const specialBonus = parseFloat(document.getElementById('special-bonus').value) || 0;
                const overtimeHours = parseFloat(document.getElementById('overtime-hours').value) || 0;
                const overtimeRate = parseFloat(document.getElementById('overtime-rate').value) || 0;
                
                // Tính lương cơ bản
                const basicSalary = days.totalDays * dailySalary;
                document.getElementById('basic-salary').textContent = formatCurrency(basicSalary) + ' VNĐ';
                
                // Tính tiền chuyên cần (chỉ khi đủ 24 ngày)
                let attendanceResult = 0;
                if (days.totalDays >= 24) {
                    attendanceResult = attendanceBonus;
                }
                document.getElementById('attendance-result').textContent = formatCurrency(attendanceResult) + ' VNĐ';
                
                // Công đoạn đặc biệt
                document.getElementById('special-result').textContent = formatCurrency(specialBonus) + ' VNĐ';
                
                // Tính tiền tăng ca
                const overtimePay = overtimeHours * overtimeRate;
                document.getElementById('overtime-result').textContent = formatCurrency(overtimePay) + ' VNĐ';
                
                // Tổng lương
                const totalSalary = basicSalary + attendanceResult + specialBonus + overtimePay;
                document.getElementById('total-salary').textContent = formatCurrency(totalSalary) + ' VNĐ';
            }
            
            // Hàm định dạng tiền tệ
            function formatCurrency(amount) {
                return amount.toFixed(0).replace(/\B(?=(\d{3})+(?!\d))/g, ".");
            }
            
            // Sự kiện thêm ngày nghỉ từ form
            document.getElementById('add-off-day-btn').addEventListener('click', function() {
                const newOffDay = document.getElementById('new-off-day').value;
                const offDayType = document.getElementById('off-day-type').value;
                
                if (!newOffDay) {
                    alert('Vui lòng chọn một ngày');
                    return;
                }
                
                // Kiểm tra xem ngày đã tồn tại chưa
                const existingIndex = offDays.findIndex(day => day.date === newOffDay);
                
                if (existingIndex !== -1) {
                    // Cập nhật loại nghỉ nếu đã tồn tại
                    offDays[existingIndex].type = offDayType;
                } else {
                    // Thêm mới ngày nghỉ
                    offDays.push({
                        date: newOffDay,
                        type: offDayType
                    });
                }
                
                updateOffDaysDisplay();
                updateCalendar();
                calculateSalary();
                
                // Reset input
                document.getElementById('new-off-day').value = '';
                
                // Animation
                const btn = this;
                btn.innerHTML = '<i class="fas fa-check"></i> <span id="add-off-day-label">Đã thêm</span>';
                btn.style.background = '#4CAF50';
                setTimeout(() => {
                    btn.innerHTML = '<i class="fas fa-plus"></i> <span id="add-off-day-label">Thêm</span>';
                    btn.style.background = '#ff6b6b';
                }, 1000);
            });
            
            // Sự kiện nút tính lương
            document.getElementById('calculate-btn').addEventListener('click', function() {
                calculateSalary();
                
                // Animation cho nút
                const btn = this;
                btn.style.transform = 'scale(0.95)';
                setTimeout(() => {
                    btn.style.transform = 'scale(1)';
                }, 200);
            });
            
            // Sự kiện thay đổi trên các input
            document.getElementById('start-date').addEventListener('change', calculateSalary);
            document.getElementById('end-date').addEventListener('change', calculateSalary);
            
            // Sử dụng debounce cho các input để tránh nhảy số liên tục
            let timeout;
            function debounceCalculate() {
                clearTimeout(timeout);
                timeout = setTimeout(calculateSalary, 500);
            }
            
            document.getElementById('daily-salary').addEventListener('input', debounceCalculate);
            document.getElementById('attendance-bonus').addEventListener('input', debounceCalculate);
            document.getElementById('special-bonus').addEventListener('input', debounceCalculate);
            document.getElementById('overtime-hours').addEventListener('input', debounceCalculate);
            document.getElementById('overtime-rate').addEventListener('input', debounceCalculate);
            
            // Sự kiện nút tháng trước
            document.getElementById('prev-month').addEventListener('click', function() {
                currentMonth--;
                if (currentMonth < 0) {
                    currentMonth = 11;
                    currentYear--;
                }
                updateCalendar();
                
                // Animation
                this.style.transform = 'scale(0.8)';
                setTimeout(() => {
                    this.style.transform = 'scale(1)';
                }, 200);
            });
            
            // Sự kiện nút tháng sau
            document.getElementById('next-month').addEventListener('click', function() {
                currentMonth++;
                if (currentMonth > 11) {
                    currentMonth = 0;
                    currentYear++;
                }
                updateCalendar();
                
                // Animation
                this.style.transform = 'scale(0.8)';
                setTimeout(() => {
                    this.style.transform = 'scale(1)';
                }, 200);
            });
            
            // ============= CHATBOT FUNCTIONALITY =============
            const chatbotToggle = document.getElementById('chatbot-toggle');
            const chatbotWindow = document.getElementById('chatbot-window');
            const chatMessages = document.getElementById('chatbot-messages');
            const chatInput = document.getElementById('chat-input');
            const sendButton = document.getElementById('send-message');
            
            // Toggle chatbot window
            chatbotToggle.addEventListener('click', function() {
                chatbotWindow.classList.toggle('active');
                document.querySelector('.chatbot-toggle .notification').style.display = 'none';
            });
            
            // Send message
            function sendMessage() {
                const message = chatInput.value.trim();
                if (message) {
                    // Add user message
                    addMessage(message, 'user');
                    
                    // Simulate bot response after delay
                    setTimeout(() => {
                        const response = getBotResponse(message.toLowerCase());
                        addMessage(response, 'bot');
                        scrollToBottom();
                    }, 1000);
                    
                    // Clear input
                    chatInput.value = '';
                }
            }
            
            // Send on button click
            sendButton.addEventListener('click', sendMessage);
            
            // Send on Enter key
            chatInput.addEventListener('keypress', function(e) {
                if (e.key === 'Enter') {
                    sendMessage();
                }
            });
            
            // Quick questions
            document.querySelectorAll('.quick-question').forEach(button => {
                button.addEventListener('click', function() {
                    const question = this.getAttribute('data-question');
                    const questionText = this.textContent;
                    
                    // Add user message
                    addMessage(questionText, 'user');
                    
                    // Simulate bot response after delay
                    setTimeout(() => {
                        const response = getBotResponse(question);
                        addMessage(response, 'bot');
                        scrollToBottom();
                    }, 1000);
                });
            });
            
            // Add message to chat
            function addMessage(text, sender) {
                const messageElement = document.createElement('div');
                messageElement.classList.add('message', sender);
                messageElement.textContent = text;
                chatMessages.appendChild(messageElement);
                scrollToBottom();
            }
            
            // Scroll to bottom of chat
            function scrollToBottom() {
                chatMessages.scrollTop = chatMessages.scrollHeight;
            }
            
            // Get bot response
            function getBotResponse(message) {
                if (message === 'how-to-use' || message.includes('cách sử dụng') || message.includes('how to use')) {
                    return "Để sử dụng ứng dụng tính lương:\n1. Chọn khoảng thời gian cần tính lương\n2. Nhập lương ngày và các khoản thưởng\n3. Nhập thông tin tăng ca (nếu có)\n4. Nhấn vào ngày trong lịch để đánh dấu ngày nghỉ\n5. Nhấn nút 'Tính lương' để xem kết quả";
                } else if (message === 'bonus-calculation' || message.includes('tiền thưởng') || message.includes('bonus')) {
                    return "Tiền chuyên cần chỉ được tính khi bạn có đủ 24 ngày công. Tiền công đoạn đặc biệt được cộng trực tiếp vào tổng lương.";
                } else if (message === 'overtime' || message.includes('tăng ca') || message.includes('overtime')) {
                    return "Tiền tăng ca được tính bằng: [Số giờ tăng ca] × [Lương tăng ca mỗi giờ]. Kết quả sẽ được cộng vào tổng lương cuối cùng.";
                } else if (message === 'day-off' || message.includes('ngày nghỉ') || message.includes('day off')) {
                    return "Bạn có thể thêm ngày nghỉ bằng cách nhấn vào ngày trong lịch hoặc nhập ngày ở phần 'Quản lý ngày nghỉ'. Có các loại nghỉ: cả ngày, nửa ngày, 1/4 ngày và 3/4 ngày.";
                } else if (message.includes('cảm ơn') || message.includes('thank')) {
                    return "Không có gì! Nếu bạn cần thêm trợ giúp, cứ hỏi nhé!";
                } else {
                    return "Xin lỗi, tôi chưa hiểu câu hỏi của bạn. Bạn có thể hỏi về cách sử dụng ứng dụng, tính tiền thưởng, tăng ca hoặc cách thêm ngày nghỉ.";
                }
            }
            
            // ============= LANGUAGE SWITCHER =============
            const langVi = document.getElementById('lang-vi');
            const langEn = document.getElementById('lang-en');
            
            // Vietnamese translations
            const viTranslations = {
                appTitle: "TÍNH LƯƠNG TRỰC QUAN",
                appSubtitle: "Giao diện siêu hiện đại với hiệu ứng chuyển động mượt mà",
                timePeriodTitle: "Chọn khoảng thời gian",
                fromDateLabel: "Từ ngày",
                toDateLabel: "Đến ngày",
                workingDaysLabel: "Ngày công:",
                daysLabel: "ngày",
                dailySalaryLabel: "Lương ngày (VNĐ)",
                bonusTitle: "Thưởng & Ngày nghỉ",
                attendanceBonusLabel: "Tiền chuyên cần (VNĐ)",
                bonusInfoText: "Tiền chuyên cần chỉ được tính khi đủ 24 ngày công",
                specialBonusLabel: "Tiền công đoạn đặc biệt (VNĐ)",
                salarySummaryTitle: "Tổng hợp lương",
                basicSalaryLabel: "Lương cơ bản:",
                attendanceResultLabel: "Tiền chuyên cần:",
                specialResultLabel: "Công đoạn đặc biệt:",
                totalSalaryLabel: "TỔNG LƯƠNG:",
                calculateBtnLabel: "TÍNH LƯƠNG",
                footerText: "© 2023 Ứng dụng Tính Lương Nâng Cao | Giao diện siêu hiện đại với hiệu ứng chuyển động mượt mà",
                chatbotTitle: "Trợ lý tính lương",
                welcomeMessage: "Xin chào! Tôi có thể giúp gì cho bạn về tính lương?",
                howToUse: "Cách sử dụng ứng dụng",
                bonusCalc: "Cách tính tiền thưởng",
                dayOff: "Cách thêm ngày nghỉ",
                overtimeTitle: "Tính lương tăng ca",
                overtimeHoursLabel: "Số giờ tăng ca",
                overtimeRateLabel: "Lương tăng ca/giờ (VNĐ)",
                overtimeResultLabel: "Tiền tăng ca:",
                offDayTitle: "Quản lý ngày nghỉ",
                offDayLabel: "ngày nghỉ",
                addOffDayLabel: "Thêm",
                noOffDays: "Chưa có ngày nghỉ nào được thêm"
            };
            
            // English translations
            const enTranslations = {
                appTitle: "SALARY CALCULATOR",
                appSubtitle: "Super modern interface with smooth animations",
                timePeriodTitle: "Select Time Period",
                fromDateLabel: "From Date",
                toDateLabel: "To Date",
                workingDaysLabel: "Working Days:",
                daysLabel: "days",
                dailySalaryLabel: "Daily Salary (VND)",
                bonusTitle: "Bonuses & Days Off",
                attendanceBonusLabel: "Attendance Bonus (VND)",
                bonusInfoText: "Attendance bonus is only calculated when you have 24 working days",
                specialBonusLabel: "Special Bonus (VND)",
                salarySummaryTitle: "Salary Summary",
                basicSalaryLabel: "Basic Salary:",
                attendanceResultLabel: "Attendance Bonus:",
                specialResultLabel: "Special Bonus:",
                totalSalaryLabel: "TOTAL SALARY:",
                calculateBtnLabel: "CALCULATE SALARY",
                footerText: "© 2023 Advanced Salary Calculator | Super modern interface with smooth animations",
                chatbotTitle: "Salary Assistant",
                welcomeMessage: "Hello! How can I help you with salary calculation?",
                howToUse: "How to use the app",
                bonusCalc: "Bonus calculation",
                dayOff: "How to add days off",
                overtimeTitle: "Overtime Calculation",
                overtimeHoursLabel: "Overtime Hours",
                overtimeRateLabel: "Overtime Rate/Hour (VND)",
                overtimeResultLabel: "Overtime Pay:",
                offDayTitle: "Manage Days Off",
                offDayLabel: "days off",
                addOffDayLabel: "Add",
                noOffDays: "No days off added yet"
            };
            
            // Set language
            function setLanguage(lang) {
                const translations = lang === 'vi' ? viTranslations : enTranslations;
                
                // Update UI elements
                document.getElementById('app-title').textContent = translations.appTitle;
                document.getElementById('app-subtitle').textContent = translations.appSubtitle;
                document.getElementById('time-period-title').textContent = translations.timePeriodTitle;
                document.getElementById('from-date-label').textContent = translations.fromDateLabel;
                document.getElementById('to-date-label').textContent = translations.toDateLabel;
                document.getElementById('working-days-label').textContent = translations.workingDaysLabel;
                document.getElementById('days-label').textContent = translations.daysLabel;
                document.getElementById('daily-salary-label').textContent = translations.dailySalaryLabel;
                document.getElementById('bonus-title').textContent = translations.bonusTitle;
                document.getElementById('attendance-bonus-label').textContent = translations.attendanceBonusLabel;
                document.getElementById('bonus-info-text').textContent = translations.bonusInfoText;
                document.getElementById('special-bonus-label').textContent = translations.specialBonusLabel;
                document.getElementById('salary-summary-title').textContent = translations.salarySummaryTitle;
                document.getElementById('basic-salary-label').textContent = translations.basicSalaryLabel;
                document.getElementById('attendance-result-label').textContent = translations.attendanceResultLabel;
                document.getElementById('special-result-label').textContent = translations.specialResultLabel;
                document.getElementById('total-salary-label').textContent = translations.totalSalaryLabel;
                document.getElementById('calculate-btn-label').textContent = translations.calculateBtnLabel;
                document.getElementById('footer-text').textContent = translations.footerText;
                document.getElementById('chatbot-title').textContent = translations.chatbotTitle;
                document.getElementById('overtime-title').textContent = translations.overtimeTitle;
                document.getElementById('overtime-hours-label').textContent = translations.overtimeHoursLabel;
                document.getElementById('overtime-rate-label').textContent = translations.overtimeRateLabel;
                document.getElementById('overtime-result-label').textContent = translations.overtimeResultLabel;
                document.getElementById('off-day-title').textContent = translations.offDayTitle;
                document.getElementById('off-day-label').textContent = translations.offDayLabel;
                document.getElementById('add-off-day-label').textContent = translations.addOffDayLabel;
                document.getElementById('no-off-days').textContent = translations.noOffDays;
                
                document.getElementById('welcome-message').innerHTML = `
                    ${translations.welcomeMessage}
                    <div class="quick-questions">
                        <button class="quick-question" data-question="how-to-use">${translations.howToUse}</button>
                        <button class="quick-question" data-question="bonus-calculation">${translations.bonusCalc}</button>
                        <button class="quick-question" data-question="overtime">${translations.overtimeTitle}</button>
                        <button class="quick-question" data-question="day-off">${translations.dayOff}</button>
                    </div>
                `;
                
                // Reattach event listeners to quick questions
                document.querySelectorAll('.quick-question').forEach(button => {
                    button.addEventListener('click', function() {
                        const question = this.getAttribute('data-question');
                        const questionText = this.textContent;
                        
                        // Add user message
                        addMessage(questionText, 'user');
                        
                        // Simulate bot response after delay
                        setTimeout(() => {
                            const response = getBotResponse(question);
                            addMessage(response, 'bot');
                            scrollToBottom();
                        }, 1000);
                    });
                });
                
                // Update active button
                langVi.classList.toggle('active', lang === 'vi');
                langEn.classList.toggle('active', lang === 'en');
            }
            
            // Event listeners for language switcher
            langVi.addEventListener('click', () => setLanguage('vi'));
            langEn.addEventListener('click', () => setLanguage('en'));
            
            // Initialize with Vietnamese
            setLanguage('vi');
            
            // Khởi tạo hiển thị
            updateCalendar();
            updateOffDaysDisplay();
            calculateSalary();
        });
    </script>
</body>
</html>
