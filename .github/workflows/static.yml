<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>三角形确定原理演示</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background: linear-gradient(135deg, #1a2a6c, #b21f1f, #fdbb2d);
            padding: 20px;
            color: #fff;
        }
        
        .container {
            display: flex;
            flex-direction: column;
            align-items: center;
            width: 100vw;
            height: 100vh;
            background: rgba(25, 25, 35, 0.9);
            overflow: hidden;
            padding: 10px;
        }
        
        .title {
            text-align: center;
            margin-bottom: 15px;
            position: relative;
            z-index: 10;
        }
        
        h1 {
            font-size: 24px;
            margin: 0 0 5px;
            color: #4facfe;
            text-shadow: 0 0 10px rgba(79, 172, 254, 0.5);
        }
        
        .subtitle {
            color: #a0a0c0;
            font-size: 14px;
        }
        
        .canvas-container {
            flex: 1;
            width: 100%;
            height: 100%;
            position: relative;
            overflow: hidden;
            border-radius: 10px;
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.4);
        }
        
        canvas {
            background: rgba(10, 15, 30, 0.8);
            cursor: grab;
            display: block;
            touch-action: none; /* 防止移动端默认触摸行为 */
            user-select: none; /* 防止选择 */
            -webkit-user-select: none;
            -moz-user-select: none;
            -ms-user-select: none;
        }
        
        canvas:active {
            cursor: grabbing;
        }
        
        .controls-info {
            position: absolute;
            top: 10px;
            left: 10px;
            background: rgba(0, 0, 0, 0.7);
            padding: 10px;
            border-radius: 5px;
            font-size: 12px;
            color: #a0a0c0;
            z-index: 10;
        }
        
        .condition-panel {
            position: absolute;
            top: 10px;
            right: 10px;
            width: 300px;
            background: rgba(25, 25, 35, 0.95);
            border-radius: 10px;
            padding: 20px;
            z-index: 10;
            border: 2px solid #4facfe;
            display: flex;
            flex-direction: column;
            gap: 15px;
        }
        
        .history-panel {
            position: absolute;
            right: 10px;
            width: 300px;
            background: rgba(25, 25, 35, 0.95);
            border-radius: 10px;
            padding: 20px;
            z-index: 10;
            border: 2px solid #a0e63c;
            display: flex;
            flex-direction: column;
            gap: 15px;
        }
        
        .panel-title {
            text-align: center;
            font-size: 16px;
            font-weight: bold;
            color: #4facfe;
            border-bottom: 1px solid #4facfe;
            padding-bottom: 10px;
            margin: 0;
        }
        
        .history-panel .panel-title {
            color: #a0e63c;
            border-bottom-color: #a0e63c;
        }
        
        .condition-display {
            background: rgba(40, 40, 60, 0.8);
            border-radius: 8px;
            padding: 15px;
            text-align: center;
            min-height: 50px;
            display: flex;
            align-items: center;
            justify-content: center;
            flex-wrap: wrap;
            gap: 8px;
        }
        
        .no-condition {
            color: #a0a0c0;
            font-style: italic;
            font-size: 13px;
        }
        
        .condition-item {
            background: rgba(79, 172, 254, 0.2);
            border: 1px solid #4facfe;
            border-radius: 16px;
            padding: 4px 10px;
            color: #4facfe;
            font-weight: bold;
            font-size: 12px;
            display: inline-block;
            white-space: nowrap;
        }
        
        .condition-item.edge {
            background: rgba(255, 204, 0, 0.2);
            border-color: #ffcc00;
            color: #ffcc00;
        }
        
        .condition-item.angle {
            background: rgba(160, 230, 60, 0.2);
            border-color: #a0e63c;
            color: #a0e63c;
        }
        
        .judge-button {
            width: 100%;
            padding: 12px;
            background: linear-gradient(to right, #4facfe, #00f2fe);
            border: none;
            border-radius: 8px;
            color: white;
            font-size: 14px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }
        
        .judge-button:hover:not(:disabled) {
            transform: translateY(-2px);
            box-shadow: 0 4px 12px rgba(79, 172, 254, 0.3);
        }
        
        .judge-button:disabled {
            background: rgba(100, 100, 140, 0.3);
            cursor: not-allowed;
            transform: none;
            box-shadow: none;
        }
        
        .judge-button.cooldown {
            opacity: 0.7;
            transform: none;
            pointer-events: none;
        }
        

        
        .success-list, .failure-list {
            display: flex;
            flex-direction: column;
            gap: 8px;
        }
        
        .list-title {
            font-size: 13px;
            font-weight: bold;
            margin-bottom: 8px;
            padding: 4px 8px;
            border-radius: 4px;
        }
        
        .list-title.success {
            background: rgba(160, 230, 60, 0.1);
            color: #a0e63c;
            border-left: 3px solid #a0e63c;
        }
        
        .list-title.failure {
            background: rgba(255, 75, 43, 0.1);
            color: #ff4b2b;
            border-left: 3px solid #ff4b2b;
        }
        
        .empty-hint {
            color: #a0a0c0;
            font-size: 12px;
            font-style: italic;
            padding: 8px;
            text-align: center;
        }
        
        .history-item {
            background: rgba(40, 40, 60, 0.6);
            border-radius: 6px;
            padding: 6px 10px;
            font-size: 11px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            gap: 8px;
        }
        
        .history-item.success {
            border-left: 3px solid #a0e63c;
        }
        
        .history-item.failure {
            border-left: 3px solid #ff4b2b;
        }
        
        .history-condition {
            font-weight: bold;
            flex: 1;
        }
        

        
        .reset-button {
            width: 100%;
            padding: 6px;
            background: rgba(100, 100, 140, 0.4);
            border: 1px solid rgba(150, 150, 180, 0.3);
            border-radius: 4px;
            color: #a0a0c0;
            font-size: 11px;
            cursor: pointer;
            transition: all 0.2s ease;
            margin-top: 10px;
        }
        
        .reset-button:hover {
            background: rgba(120, 120, 160, 0.5);
            color: #c0c0d0;
        }
        
        /* 动画效果 */
        @keyframes successFlash {
            0% { background: linear-gradient(135deg, #1a2a6c, #b21f1f, #fdbb2d); }
            50% { background: linear-gradient(135deg, #a0e63c, #4facfe, #00f2fe); }
            100% { background: linear-gradient(135deg, #1a2a6c, #b21f1f, #fdbb2d); }
        }
        
        @keyframes failureShake {
            0%, 100% { transform: translateX(0); }
            25% { transform: translateX(-5px); }
            75% { transform: translateX(5px); }
        }
        
        .triangle-info {
            position: absolute;
            bottom: 10px;
            right: 10px;
            background: rgba(30, 30, 45, 0.8);
            padding: 10px;
            border-radius: 8px;
            font-size: 12px;
            line-height: 1.3;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
            max-width: 200px;
            z-index: 10;
        }
        
        .highlight {
            color: #4facfe;
            font-weight: bold;
        }
        
        /* 面板标题头部样式 */
        .panel-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
        }
        
        /* 总结按钮样式 */
        .summary-button {
            padding: 4px 8px;
            background: rgba(160, 230, 60, 0.1);
            border: 1px solid rgba(160, 230, 60, 0.3);
            border-radius: 4px;
            color: #a0e63c;
            font-size: 11px;
            font-weight: normal;
            cursor: pointer;
            transition: all 0.2s ease;
            opacity: 0.7;
        }
        
        .summary-button:hover {
            opacity: 1;
            background: rgba(160, 230, 60, 0.15);
            border-color: rgba(160, 230, 60, 0.5);
        }
        
        /* 模态框样式 */
        .modal-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            background: rgba(0, 0, 0, 0.8);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 1000;
            backdrop-filter: blur(5px);
            opacity: 0;
            transition: opacity 0.3s ease;
        }
        
        .modal-overlay.show {
            opacity: 1;
        }
        
        .modal-content {
            background: linear-gradient(135deg, rgba(245, 248, 255, 0.95), rgba(240, 245, 255, 0.95));
            backdrop-filter: blur(20px);
            border-radius: 20px;
            width: 90%;
            max-width: 1000px;
            max-height: 80vh;
            overflow: hidden;
            box-shadow: 0 25px 50px rgba(79, 172, 254, 0.15);
            border: 1px solid rgba(79, 172, 254, 0.2);
        }
        
        .modal-header {
            background: rgba(79, 172, 254, 0.1);
            padding: 20px 30px;
            border-bottom: 1px solid rgba(79, 172, 254, 0.2);
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .modal-header h2 {
            color: #2d3748;
            margin: 0;
            font-size: 24px;
            font-weight: 600;
        }
        
        .modal-close {
            background: rgba(255, 255, 255, 0.8);
            border: none;
            color: #718096;
            font-size: 20px;
            cursor: pointer;
            padding: 8px;
            border-radius: 50%;
            transition: all 0.3s ease;
            width: 36px;
            height: 36px;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        
        .modal-close:hover {
            background: rgba(255, 75, 43, 0.1);
            color: #ff4b2b;
            transform: scale(1.1);
        }
        
        .modal-body {
            padding: 30px;
            overflow-y: auto;
            max-height: calc(80vh - 100px);
        }
        
        .summary-columns {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 25px;
        }
        
        .summary-column {
            border-radius: 16px;
            padding: 24px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
            border: 1px solid;
        }
        
        .success-column {
            background: linear-gradient(135deg, rgba(72, 187, 120, 0.08), rgba(72, 187, 120, 0.05));
            border-color: rgba(72, 187, 120, 0.2);
            border-left: 4px solid #48bb78;
        }
        
        .failure-column {
            background: linear-gradient(135deg, rgba(245, 101, 101, 0.08), rgba(245, 101, 101, 0.05));
            border-color: rgba(245, 101, 101, 0.2);
            border-left: 4px solid #f56565;
        }
        
        .summary-column h3 {
            margin: 0 0 20px;
            font-size: 18px;
            text-align: center;
            padding-bottom: 12px;
            border-bottom: 1px solid rgba(0, 0, 0, 0.1);
            font-weight: 600;
        }
        
        .success-column h3 {
            color: #2f855a;
        }
        
        .failure-column h3 {
            color: #c53030;
        }
        
        .summary-content {
            display: flex;
            flex-direction: column;
            gap: 15px;
        }
        
        .empty-summary {
            text-align: center;
            color: #718096;
            font-style: italic;
            padding: 24px;
            border-radius: 12px;
            border: 1px dashed;
        }
        
        .success-column .empty-summary {
            background: rgba(72, 187, 120, 0.05);
            border-color: rgba(72, 187, 120, 0.3);
            color: #2f855a;
        }
        
        .failure-column .empty-summary {
            background: rgba(245, 101, 101, 0.05);
            border-color: rgba(245, 101, 101, 0.3);
            color: #c53030;
        }
        
        .condition-summary-item {
            border-radius: 12px;
            padding: 16px;
            border: 1px solid;
            transition: transform 0.2s ease, box-shadow 0.2s ease;
        }
        
        .condition-summary-item.success {
            background: linear-gradient(135deg, rgba(72, 187, 120, 0.12), rgba(72, 187, 120, 0.08));
            border-color: rgba(72, 187, 120, 0.25);
            border-left: 4px solid #48bb78;
            box-shadow: 0 2px 8px rgba(72, 187, 120, 0.15);
        }
        
        .condition-summary-item.success:hover {
            transform: translateY(-1px);
            box-shadow: 0 4px 12px rgba(72, 187, 120, 0.25);
            background: linear-gradient(135deg, rgba(72, 187, 120, 0.15), rgba(72, 187, 120, 0.10));
        }
        
        .condition-summary-item.failure {
            background: linear-gradient(135deg, rgba(245, 101, 101, 0.12), rgba(245, 101, 101, 0.08));
            border-color: rgba(245, 101, 101, 0.25);
            border-left: 4px solid #f56565;
            box-shadow: 0 2px 8px rgba(245, 101, 101, 0.15);
        }
        
        .condition-summary-item.failure:hover {
            transform: translateY(-1px);
            box-shadow: 0 4px 12px rgba(245, 101, 101, 0.25);
            background: linear-gradient(135deg, rgba(245, 101, 101, 0.15), rgba(245, 101, 101, 0.10));
        }
        
        .condition-title {
            font-size: 15px;
            font-weight: 600;
            margin-bottom: 8px;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        
        .condition-title.success {
            color: #22543d;
        }
        
        .condition-title.failure {
            color: #9b2c2c;
        }
        
        .condition-explanation {
            color: #4a5568;
            font-size: 13px;
            line-height: 1.5;
            margin-top: 6px;
        }
        
        .condition-badge {
            border-radius: 8px;
            padding: 3px 8px;
            font-size: 11px;
            font-weight: 500;
            border: 1px solid;
        }
        
        .condition-summary-item.success .condition-badge {
            background: rgba(72, 187, 120, 0.15);
            border-color: rgba(72, 187, 120, 0.4);
            color: #22543d;
        }
        
        .condition-summary-item.failure .condition-badge {
            background: rgba(245, 101, 101, 0.15);
            border-color: rgba(245, 101, 101, 0.4);
            color: #9b2c2c;
        }
        
        /* 重新开始教学按钮样式 */
        .restart-teaching-btn {
            position: fixed;
            bottom: 20px;
            left: 20px;
            background: linear-gradient(135deg, rgba(255, 248, 245, 0.95), rgba(255, 245, 240, 0.95));
            border: 1px solid rgba(239, 68, 68, 0.3);
            border-radius: 12px;
            padding: 12px 16px;
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            gap: 8px;
            box-shadow: 0 4px 12px rgba(239, 68, 68, 0.1);
            backdrop-filter: blur(10px);
            z-index: 100;
            font-family: inherit;
        }
        
        .restart-teaching-btn:hover {
            background: linear-gradient(135deg, rgba(255, 245, 240, 1), rgba(255, 240, 235, 1));
            border-color: rgba(239, 68, 68, 0.5);
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(239, 68, 68, 0.15);
        }
        
        .restart-icon {
            font-size: 16px;
            transition: transform 0.3s ease;
        }
        
        .restart-teaching-btn:hover .restart-icon {
            transform: rotate(180deg);
        }
        
        .restart-text {
            color: #ef4444;
            font-size: 13px;
            font-weight: 500;
        }
        
        /* 自定义确认对话框样式 */
        .custom-confirm-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            background: rgba(0, 0, 0, 0.6);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 2000;
            backdrop-filter: blur(3px);
        }
        
        .custom-confirm-content {
            background: linear-gradient(135deg, rgba(255, 248, 245, 0.98), rgba(255, 245, 240, 0.98));
            border-radius: 16px;
            width: 90%;
            max-width: 480px;
            box-shadow: 0 20px 40px rgba(239, 68, 68, 0.15);
            border: 1px solid rgba(239, 68, 68, 0.2);
            backdrop-filter: blur(10px);
            overflow: hidden;
        }
        
        .custom-confirm-header {
            background: rgba(239, 68, 68, 0.1);
            padding: 20px 24px;
            border-bottom: 1px solid rgba(239, 68, 68, 0.15);
            display: flex;
            align-items: center;
            gap: 12px;
        }
        
        .confirm-icon {
            font-size: 24px;
        }
        
        .custom-confirm-header h3 {
            margin: 0;
            color: #dc2626;
            font-size: 18px;
            font-weight: 600;
        }
        
        .custom-confirm-body {
            padding: 24px;
            color: #374151;
            line-height: 1.6;
        }
        
        .custom-confirm-body p {
            margin: 0 0 12px 0;
            font-size: 14px;
        }
        
        .custom-confirm-body ul {
            margin: 12px 0;
            padding-left: 20px;
        }
        
        .custom-confirm-body li {
            margin: 6px 0;
            font-size: 13px;
        }
        
        .warning-text {
            background: rgba(239, 68, 68, 0.08);
            padding: 12px;
            border-radius: 8px;
            border-left: 4px solid #ef4444;
            font-weight: 500;
            color: #dc2626;
            margin-top: 16px !important;
        }
        
        .custom-confirm-footer {
            background: rgba(249, 250, 251, 0.8);
            padding: 16px 24px;
            border-top: 1px solid rgba(229, 231, 235, 0.8);
            display: flex;
            justify-content: flex-end;
            gap: 12px;
        }
        
        .confirm-btn {
            padding: 10px 20px;
            border-radius: 8px;
            font-size: 14px;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.2s ease;
            border: 1px solid;
            font-family: inherit;
        }
        
        .cancel-btn {
            background: rgba(255, 255, 255, 0.9);
            border-color: rgba(156, 163, 175, 0.5);
            color: #6b7280;
        }
        
        .cancel-btn:hover {
            background: rgba(249, 250, 251, 1);
            border-color: rgba(156, 163, 175, 0.8);
            color: #4b5563;
        }
        
        .confirm-btn-primary {
            background: linear-gradient(135deg, #ef4444, #dc2626);
            border-color: #dc2626;
            color: white;
        }
        
        .confirm-btn-primary:hover {
            background: linear-gradient(135deg, #dc2626, #b91c1c);
            border-color: #b91c1c;
            transform: translateY(-1px);
            box-shadow: 0 4px 12px rgba(239, 68, 68, 0.25);
        }
        
        /* 小屏幕设备优化 (手机竖屏) */
        @media (max-width: 480px) {
            .container {
                flex-direction: column;
                padding: 5px;
            }
            
            .title {
                margin-bottom: 5px;
            }
            
            h1 {
                font-size: 18px;
                margin: 0;
            }
            
            .subtitle {
                font-size: 12px;
            }
            
            .canvas-container {
                flex: 1;
                height: 60vh; /* 限制画布高度，为面板留出空间 */
                min-height: 300px;
            }
            
            /* 隐藏桌面版面板 */
            .canvas-container .condition-panel,
            .canvas-container .history-panel,
            .canvas-container .triangle-info,
            .canvas-container .restart-teaching-btn,
            .canvas-container .controls-info {
                display: none !important;
            }
            
            /* 显示移动端面板 */
            .mobile-panels {
                display: block !important;
            }
            
            /* 移动端面板样式 */
            .mobile-panels .condition-panel,
            .mobile-panels .history-panel {
                position: relative;
                top: auto;
                right: auto;
                bottom: auto;
                left: auto;
                width: 100%;
                margin: 5px 0;
                padding: 12px;
                font-size: 12px;
            }
            
            .mobile-panels .panel-title {
                font-size: 14px;
                padding-bottom: 8px;
            }
            
            .mobile-panels .condition-display {
                padding: 10px;
                min-height: 35px;
            }
            
            .mobile-panels .condition-item {
                font-size: 10px;
                padding: 2px 6px;
            }
            
            .mobile-panels .judge-button {
                padding: 8px;
                font-size: 12px;
            }
            
            .mobile-panels .reset-button {
                padding: 4px;
                font-size: 9px;
            }
            
            .mobile-panels .controls-info,
            .mobile-panels .triangle-info {
                position: relative;
                top: auto;
                left: auto;
                bottom: auto;
                right: auto;
                width: 100%;
                margin: 5px 0;
                font-size: 10px;
                padding: 8px;
                max-width: none;
            }
            
            .mobile-panels .restart-teaching-btn {
                position: relative;
                bottom: auto;
                left: auto;
                width: 100%;
                margin: 5px 0;
                padding: 8px 12px;
            }
            
            .mobile-panels .restart-text {
                font-size: 11px;
            }
            
            .mobile-panels .panel-header {
                flex-direction: row;
                align-items: center;
                gap: 8px;
                justify-content: space-between;
            }
            
            .mobile-panels .summary-button {
                align-self: auto;
                font-size: 10px;
                padding: 4px 8px;
            }
        }
        
        /* 中等屏幕设备优化 (平板竖屏) */
        @media (min-width: 481px) and (max-width: 768px) {
            .condition-panel, .history-panel {
                width: 250px;
                padding: 15px;
                font-size: 13px;
            }
            
            .panel-title {
                font-size: 14px;
            }
            
            .condition-display {
                padding: 12px;
                min-height: 40px;
            }
            
            .condition-item {
                font-size: 11px;
                padding: 3px 8px;
            }
            
            .judge-button {
                padding: 10px;
                font-size: 13px;
            }
            
            .reset-button {
                padding: 5px;
                font-size: 10px;
            }
            
            .controls-info {
                font-size: 11px;
                padding: 8px;
                max-width: 180px;
            }
            
            .triangle-info {
                font-size: 11px;
                padding: 8px;
                max-width: 150px;
            }
            
            .restart-teaching-btn {
                bottom: 15px;
                left: 15px;
                padding: 10px 12px;
            }
            
            .restart-text {
                font-size: 12px;
            }
            
            .panel-header {
                flex-direction: column;
                align-items: flex-start;
                gap: 8px;
            }
            
            .summary-button {
                align-self: flex-end;
            }
        }
        
        /* 通用移动端优化 */
        @media (max-width: 768px) {
            .summary-columns {
                grid-template-columns: 1fr;
                gap: 20px;
            }
            
            .modal-content {
                width: 95%;
                margin: 10px;
            }
            
            .modal-header {
                padding: 15px 20px;
            }
            
            .modal-header h2 {
                font-size: 20px;
            }
            
            .modal-body {
                padding: 20px;
            }
            
            /* 自定义确认对话框移动端优化 */
            .custom-confirm-content {
                width: 95%;
                max-width: 400px;
            }
            
            .custom-confirm-header {
                padding: 16px 20px;
            }
            
            .custom-confirm-header h3 {
                font-size: 16px;
            }
            
            .custom-confirm-body {
                padding: 20px;
            }
            
            .custom-confirm-footer {
                padding: 12px 20px;
                flex-direction: column;
                gap: 8px;
            }
            
            .confirm-btn {
                width: 100%;
                padding: 12px;
            }
        }
        
        /* 触摸设备优化 */
        @media (hover: none) and (pointer: coarse) {
            .condition-panel, .history-panel {
                /* 增大触摸目标 */
            }
            
            .judge-button {
                min-height: 44px; /* iOS推荐的最小触摸目标 */
            }
            
            .reset-button {
                min-height: 36px;
            }
            
            .summary-button {
                min-height: 32px;
                padding: 6px 10px;
            }
            
            .restart-teaching-btn {
                min-height: 44px;
                min-width: 44px;
            }
            
            /* 移除悬停效果 */
            .judge-button:hover:not(:disabled),
            .reset-button:hover,
            .summary-button:hover,
            .restart-teaching-btn:hover,
            .confirm-btn:hover,
            .condition-summary-item.success:hover,
            .condition-summary-item.failure:hover {
                transform: none;
                box-shadow: initial;
                background: initial;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="title">
            <h1>讯飞三角形全等判定教学工具</h1>
        </div>
        
        <div class="canvas-container">
            <canvas id="triangleCanvas"></canvas>
            
            <div class="controls-info">
                <div>拖拽画布：左键拖动空白区域</div>
                <div>缩放画布：滚轮缩放</div>
                <div>拖动顶点：拖动A/B/C顶点</div>
                <div>固定角度：双击或长按顶点(红色描边)</div>
                <div>固定边长：双击或长按边(红色实线)</div>
                <div>取消固定：再次双击或长按</div>
                <div style="border-top: 1px solid rgba(255,255,255,0.2); margin-top: 8px; padding-top: 8px;">
                    <div>画笔工具：<button id="toggle-drawing" style="margin-left: 5px;">开启画笔</button></div>
                    <div id="drawing-controls" style="display: none; margin-top: 5px;">
                        <div>颜色：<input type="color" id="brush-color" value="#ff6b6b" style="width: 30px; height: 20px; margin-left: 5px;"></div>
                        <div style="margin-top: 3px;">大小：<input type="range" id="brush-size" min="1" max="10" value="3" style="width: 60px; margin-left: 5px;"></div>
                        <div style="margin-top: 3px;">
                            <button id="toggle-eraser" style="margin-right: 5px;">🧽 橡皮擦</button>
                            <button id="clear-drawings">清除画笔</button>
                        </div>
                        <div id="eraser-controls" style="display: none; margin-top: 3px;">
                            <div>橡皮擦大小：<input type="range" id="eraser-size" min="10" max="50" value="20" style="width: 60px; margin-left: 5px;"></div>
                        </div>
                    </div>
                </div>
            </div>
            
            <!-- 当前条件面板 -->
            <div class="condition-panel">
                <div class="panel-title">当前固定条件</div>
                <div class="condition-display" id="condition-display">
                    <span class="no-condition">尚未固定任何条件</span>
                </div>
                <button class="judge-button" id="judge-button" disabled>
                    🔍 判定是否能确定三角形
                </button>
                <div style="display: flex; gap: 8px;">
                    <button class="reset-button" id="reset-congruence" style="flex: 1;">重置固定</button>
                    <button class="reset-button" id="reset-triangle" style="flex: 1;">重置三角形</button>
                </div>
            </div>
            
            <!-- 探索记录面板 -->
            <div class="history-panel">
                <div class="panel-header">
                    <div class="panel-title">探索记录</div>
                    <button class="summary-button" id="summary-button">📋 总结</button>
                </div>
                <div class="success-list" id="success-list">
                    <div class="list-title success">✅ 成功条件</div>
                    <div class="empty-hint">还没有发现成功的条件</div>
                </div>
                <div class="failure-list" id="failure-list">
                    <div class="list-title failure">❌ 失败条件</div>
                    <div class="empty-hint">还没有尝试失败的条件</div>
                </div>
            </div>
            
            <div class="triangle-info" id="triangleInfo">
                <div>三角形 ABC</div>
                <div>边 a (BC): <span id="sideA">--</span></div>
                <div>边 b (AC): <span id="sideB">--</span></div>
                <div>边 c (AB): <span id="sideC">--</span></div>
                <div>角 A: <span id="angleA">--</span></div>
                <div>角 B: <span id="angleB">--</span></div>
                <div>角 C: <span id="angleC">--</span></div>
            </div>
            
            <!-- 重新开始教学按钮 -->
            <button class="restart-teaching-btn" id="restart-teaching">
                <span class="restart-icon">🔄</span>
                <span class="restart-text">重新开始教学</span>
            </button>
        </div>
        
        <!-- 移动端面板容器 -->
        <div class="mobile-panels" style="display: none;">
            <!-- 当前条件面板 (移动端) -->
            <div class="condition-panel mobile-condition-panel">
                <div class="panel-title">当前固定条件</div>
                <div class="condition-display" id="mobile-condition-display">
                    <span class="no-condition">尚未固定任何条件</span>
                </div>
                <button class="judge-button" id="mobile-judge-button" disabled>
                    🔍 判定是否能确定三角形
                </button>
                <div style="display: flex; gap: 8px;">
                    <button class="reset-button" id="mobile-reset-congruence" style="flex: 1;">重置固定</button>
                    <button class="reset-button" id="mobile-reset-triangle" style="flex: 1;">重置三角形</button>
                </div>
            </div>
            
            <!-- 探索记录面板 (移动端) -->
            <div class="history-panel mobile-history-panel">
                <div class="panel-header">
                    <div class="panel-title">探索记录</div>
                    <button class="summary-button" id="mobile-summary-button">📋 总结</button>
                </div>
                <div class="success-list" id="mobile-success-list">
                    <div class="list-title success">✅ 成功条件</div>
                    <div class="empty-hint">还没有发现成功的条件</div>
                </div>
                <div class="failure-list" id="mobile-failure-list">
                    <div class="list-title failure">❌ 失败条件</div>
                    <div class="empty-hint">还没有尝试失败的条件</div>
                </div>
            </div>
            
            <div class="triangle-info mobile-triangle-info" id="mobileTriangleInfo">
                <div>三角形 ABC</div>
                <div>边 a (BC): <span id="mobile-sideA">--</span></div>
                <div>边 b (AC): <span id="mobile-sideB">--</span></div>
                <div>边 c (AB): <span id="mobile-sideC">--</span></div>
                <div>角 A: <span id="mobile-angleA">--</span></div>
                <div>角 B: <span id="mobile-angleB">--</span></div>
                <div>角 C: <span id="mobile-angleC">--</span></div>
            </div>
            
            <!-- 重新开始教学按钮 (移动端) -->
            <button class="restart-teaching-btn mobile-restart-teaching-btn" id="mobile-restart-teaching">
                <span class="restart-icon">🔄</span>
                <span class="restart-text">重新开始教学</span>
            </button>
            
            <div class="controls-info mobile-controls-info">
                <div>拖拽画布：单指拖动空白区域</div>
                <div>缩放画布：双指缩放</div>
                <div>拖动顶点：拖动A/B/C顶点</div>
                <div>固定角度：长按顶点(红色描边)</div>
                <div>固定边长：长按边(红色实线)</div>
                <div>取消固定：再次长按</div>
                <div style="border-top: 1px solid rgba(255,255,255,0.2); margin-top: 8px; padding-top: 8px;">
                    <div>画笔工具：<button id="mobile-toggle-drawing" style="margin-left: 5px;">开启画笔</button></div>
                    <div id="mobile-drawing-controls" style="display: none; margin-top: 5px;">
                        <div>颜色：<input type="color" id="mobile-brush-color" value="#ff6b6b" style="width: 30px; height: 20px; margin-left: 5px;"></div>
                        <div style="margin-top: 3px;">大小：<input type="range" id="mobile-brush-size" min="1" max="10" value="3" style="width: 60px; margin-left: 5px;"></div>
                        <div style="margin-top: 3px;">
                            <button id="mobile-toggle-eraser" style="margin-right: 5px;">🧽 橡皮擦</button>
                            <button id="mobile-clear-drawings">清除画笔</button>
                        </div>
                        <div id="mobile-eraser-controls" style="display: none; margin-top: 3px;">
                            <div>橡皮擦大小：<input type="range" id="mobile-eraser-size" min="10" max="50" value="20" style="width: 60px; margin-left: 5px;"></div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        
        <!-- 自定义确认对话框 -->
        <div class="custom-confirm-overlay" id="custom-confirm" style="display: none;">
            <div class="custom-confirm-content">
                <div class="custom-confirm-header">
                    <span class="confirm-icon">⚠️</span>
                    <h3>重新开始教学确认</h3>
                </div>
                <div class="custom-confirm-body">
                    <p>这个操作将会：</p>
                    <ul>
                        <li>清除所有探索记录（成功和失败的条件）</li>
                        <li>重置三角形到初始状态</li>
                        <li>清除所有画笔标注</li>
                        <li>清除所有固定的边和角</li>
                    </ul>
                    <p class="warning-text">⚠️ 老师注意：此操作不可撤销，将丢失学生的所有探索进度！</p>
                </div>
                <div class="custom-confirm-footer">
                    <button class="confirm-btn cancel-btn" id="confirm-cancel">取消</button>
                    <button class="confirm-btn confirm-btn-primary" id="confirm-ok">确认清除数据</button>
                </div>
            </div>
        </div>
        
        <!-- 探索总结模态框 -->
        <div class="modal-overlay" id="summary-modal" style="display: none;">
            <div class="modal-content">
                <div class="modal-header">
                    <h2>🎯 三角形全等判定探索总结</h2>
                    <button class="modal-close" id="modal-close">✕</button>
                </div>
                <div class="modal-body">
                    <div class="summary-columns">
                        <div class="summary-column success-column">
                            <h3>✅ 成功的判定条件</h3>
                            <div class="summary-content" id="success-summary">
                                <div class="empty-summary">还没有发现成功的条件，继续探索吧！</div>
                            </div>
                        </div>
                        <div class="summary-column failure-column">
                            <h3>❌ 失败的判定条件</h3>
                            <div class="summary-content" id="failure-summary">
                                <div class="empty-summary">还没有尝试失败的条件，勇敢尝试吧！</div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // 获取Canvas元素和上下文
        const canvas = document.getElementById('triangleCanvas');
        const ctx = canvas.getContext('2d');
        
        // 三角形对象
        let triangle = null;
        
        // 画布变换状态
        let transform = {
            x: 0,  // 平移X
            y: 0,  // 平移Y
            scale: 1  // 缩放比例
        };
        
        // 拖拽状态
        let isDragging = false;
        let isVertexDragging = false;
        let dragStartPos = { x: 0, y: 0 };
        let draggedVertex = null;
        
        // 长按状态
        let longPressTimer = null;
        let longPressTarget = null;
        let longPressStartPos = { x: 0, y: 0 };
        let isLongPressed = false;
        const LONG_PRESS_DURATION = 600; // 长按持续时间（毫秒）- 减少到600ms更适合触屏
        const LONG_PRESS_TOLERANCE = 15; // 长按期间允许的移动距离 - 增加容忍度
        
        // 移动端触摸状态
        let touchStartTime = 0;
        let touchStartPos = { x: 0, y: 0 };
        let lastTouchPos = { x: 0, y: 0 };
        let touchCount = 0;
        let lastTouchTime = 0;
        let pinchStartDistance = 0;
        let pinchStartScale = 1;
        const DOUBLE_TAP_DELAY = 300; // 双击检测时间间隔
        
        // 固定状态
        let fixedAngles = {
            A: false,
            B: false,
            C: false
        };
        
        let fixedEdges = {
            a: false, // BC边
            b: false, // AC边
            c: false  // AB边
        };
        
        // 固定时的初始值
        let initialAngles = {};
        let initialEdgeLengths = {};
        
        // 探索学习状态
        let successfulConditions = new Set(); // 成功的条件组合
        let failedConditions = new Set(); // 失败的条件组合
        let currentConditionString = ''; // 当前条件字符串
        let isJudging = false; // 是否正在进行判定动画
        
        // localStorage 键名
        const STORAGE_KEY_SUCCESS = 'triangle_exploration_success';
        const STORAGE_KEY_FAILURE = 'triangle_exploration_failure';
        
        // 判定按钮防重复点击
        let lastJudgeTime = 0;
        const JUDGE_COOLDOWN = 1000; // 判定冷却时间（毫秒）
        
        // 当前判定结果显示状态
        let currentJudgeResult = null; // null, 'success', 'failure'
        let judgeResultCondition = null; // 产生当前判定结果的条件
        
        // 画笔工具状态
        let drawingMode = false; // 是否处于绘画模式
        let eraserMode = false; // 是否处于橡皮擦模式
        let isDrawing = false; // 是否正在绘画
        let isErasing = false; // 是否正在擦除
        let drawingPaths = []; // 存储绘画路径
        let currentPath = null; // 当前正在绘制的路径
        let brushColor = '#ff6b6b'; // 画笔颜色
        let brushSize = 3; // 画笔大小
        let eraserSize = 20; // 橡皮擦大小
        
        // 约束显示状态
        let persistentConstraints = null; // 持久显示的约束（画笔模式时保持）
        let persistentDraggedVertex = null; // 持久显示约束的顶点
        
        // 鼠标位置跟踪（用于橡皮擦预览）
        let mousePos = null;
        
        // 初始化
        function init() {
            // 设置画布大小为整个容器大小
            const container = document.querySelector('.canvas-container');
            const rect = container.getBoundingClientRect();
            
            canvas.width = rect.width;
            canvas.height = rect.height;
            
            // 设置画布显示大小
            canvas.style.width = rect.width + 'px';
            canvas.style.height = rect.height + 'px';
            
            // 创建等边三角形
            createEquilateralTriangle();
            
            // 添加事件监听器
            addEventListeners();
            
            // 初始化探索面板
            initExplorationPanel();
            
            // 初始化画笔工具
            initDrawingTool();
            
            // 调整面板位置
            adjustPanelPositions();
            
            // 绘制
            drawScene();
        }
        
        // 添加事件监听器
        function addEventListeners() {
            // 鼠标事件
            canvas.addEventListener('mousedown', handleMouseDown);
            canvas.addEventListener('mousemove', handleMouseMove);
            canvas.addEventListener('mouseup', handleMouseUp);
            canvas.addEventListener('mouseleave', handleMouseLeave);
            canvas.addEventListener('dblclick', handleDoubleClick);
            
            // 触摸事件
            canvas.addEventListener('touchstart', handleTouchStart, { passive: false });
            canvas.addEventListener('touchmove', handleTouchMove, { passive: false });
            canvas.addEventListener('touchend', handleTouchEnd, { passive: false });
            canvas.addEventListener('touchcancel', handleTouchEnd, { passive: false });
            
            // 滚轮缩放
            canvas.addEventListener('wheel', handleWheel);
            
            // 防止右键菜单
            canvas.addEventListener('contextmenu', e => e.preventDefault());
        }
        
        // 获取触摸点坐标
        function getTouchPos(e) {
            const rect = canvas.getBoundingClientRect();
            const touch = e.touches[0] || e.changedTouches[0];
            return {
                clientX: touch.clientX - rect.left,
                clientY: touch.clientY - rect.top,
                rawX: touch.clientX,
                rawY: touch.clientY
            };
        }
        
        // 计算两点间距离（用于缩放手势）
        function getTouchDistance(e) {
            if (e.touches.length < 2) return 0;
            const touch1 = e.touches[0];
            const touch2 = e.touches[1];
            return Math.sqrt(
                Math.pow(touch2.clientX - touch1.clientX, 2) + 
                Math.pow(touch2.clientY - touch1.clientY, 2)
            );
        }
        
        // 触摸开始事件
        function handleTouchStart(e) {
            e.preventDefault();
            
            const currentTime = Date.now();
            touchCount = e.touches.length;
            
            if (touchCount === 1) {
                // 单指触摸
                const pos = getTouchPos(e);
                touchStartTime = currentTime;
                touchStartPos = { x: pos.clientX, y: pos.clientY };
                lastTouchPos = { x: pos.clientX, y: pos.clientY };
                
                // 检测双击
                if (currentTime - lastTouchTime < DOUBLE_TAP_DELAY) {
                    handleTouchDoubleClick(pos);
                    return;
                }
                lastTouchTime = currentTime;
                
                // 转换为画布坐标进行检测
                const canvasPos = screenToCanvas(pos.clientX, pos.clientY);
                
                // 如果处于绘画模式，开始绘画（不检测顶点或边）
                if (drawingMode) {
                    if (eraserMode) {
                        // 橡皮擦模式
                        isErasing = true;
                        eraseAtPosition(canvasPos.x, canvasPos.y);
                    } else {
                        // 画笔模式
                        isDrawing = true;
                        currentPath = {
                            points: [{ x: canvasPos.x, y: canvasPos.y }],
                            color: brushColor,
                            size: brushSize
                        };
                    }
                    
                    // 画笔模式下不处理顶点或边的交互
                    return;
                }
                
                // 重置长按状态
                isLongPressed = false;
                clearLongPressTimer();
                
                // 检查是否点击在顶点上
                const clickedVertex = getClickedVertex(canvasPos.x, canvasPos.y);
                
                if (clickedVertex) {
                    // 开始长按检测（使用屏幕坐标）
                    startLongPress('vertex', clickedVertex, pos.clientX, pos.clientY);
                    
                    // 准备拖拽顶点
                    draggedVertex = clickedVertex;
                    isVertexDragging = false; // 初始状态，等待长按检测完成或移动触发
                } else {
                    // 检查是否点击在边上
                    const clickedEdge = getClickedEdge(canvasPos.x, canvasPos.y);
                    
                    if (clickedEdge) {
                        // 开始长按检测
                        startLongPress('edge', clickedEdge, pos.clientX, pos.clientY);
                    } else {
                        // 开始拖拽画布
                        isDragging = true;
                        dragStartPos = { x: pos.clientX, y: pos.clientY };
                    }
                }
                
            } else if (touchCount === 2) {
                // 双指触摸（缩放手势）
                pinchStartDistance = getTouchDistance(e);
                pinchStartScale = transform.scale;
                
                // 取消单指操作
                clearLongPressTimer();
                isDragging = false;
                isVertexDragging = false;
                draggedVertex = null;
                isDrawing = false;
                currentPath = null;
            }
        }
        
        // 触摸移动事件
        function handleTouchMove(e) {
            e.preventDefault();
            
            if (touchCount === 1) {
                // 单指移动
                const pos = getTouchPos(e);
                const canvasPos = screenToCanvas(pos.clientX, pos.clientY);
                
                // 如果正在绘画，添加点到当前路径
                if (isDrawing && currentPath) {
                    currentPath.points.push({ x: canvasPos.x, y: canvasPos.y });
                    drawScene();
                    lastTouchPos = { x: pos.clientX, y: pos.clientY };
                    return;
                }
                
                // 如果正在擦除，继续擦除
                if (isErasing) {
                    eraseAtPosition(canvasPos.x, canvasPos.y);
                    lastTouchPos = { x: pos.clientX, y: pos.clientY };
                    return;
                }
                
                // 检查长按期间是否移动过多
                if (longPressTimer && !isLongPressed) {
                    const dx = pos.clientX - longPressStartPos.x;
                    const dy = pos.clientY - longPressStartPos.y;
                    const distance = Math.sqrt(dx * dx + dy * dy);
                    
                    if (distance > LONG_PRESS_TOLERANCE) {
                        // 移动距离过大，取消长按，开始拖拽
                        clearLongPressTimer();
                        if (longPressTarget && longPressTarget.type === 'vertex') {
                            isVertexDragging = true;
                        }
                    }
                }
                
                // 处理顶点拖拽
                if ((isVertexDragging || (draggedVertex && !longPressTimer)) && draggedVertex && !isLongPressed) {
                    isVertexDragging = true;
                    
                    // 特殊逻辑：AAA情况下任何顶点都可以缩放
                    if (canPerformAAAScaling()) {
                        scaleTriangleProportionally(draggedVertex, canvasPos);
                    } 
                    // 两角固定且可以缩放（非ASA情况），拖拽第三个顶点时进行等比缩放
                    else if (canPerformTwoAngleScaling() && draggedVertex === getUnfixedAngle()) {
                        scaleTriangleProportionally(draggedVertex, canvasPos);
                    } else if (fixedAngles[draggedVertex]) {
                        // 如果拖拽的顶点角度被固定，则拖拽整个三角形而不是单个顶点
                        const dx = canvasPos.x - triangle[draggedVertex].x;
                        const dy = canvasPos.y - triangle[draggedVertex].y;
                        
                        // 移动整个三角形
                        triangle.A.x += dx;
                        triangle.A.y += dy;
                        triangle.B.x += dx;
                        triangle.B.y += dy;
                        triangle.C.x += dx;
                        triangle.C.y += dy;
                    } else {
                        // 普通拖拽顶点
                        applyConstraints(draggedVertex, canvasPos);
                    }
                    
                    drawScene();
                    updateTriangleInfo();
                    updateConditionDisplay();
                } else if (isDragging) {
                    // 拖拽画布
                    const dx = pos.clientX - dragStartPos.x;
                    const dy = pos.clientY - dragStartPos.y;
                    
                    transform.x += dx;
                    transform.y += dy;
                    
                    dragStartPos = { x: pos.clientX, y: pos.clientY };
                    drawScene();
                }
                
                lastTouchPos = { x: pos.clientX, y: pos.clientY };
                
            } else if (touchCount === 2 && e.touches.length === 2) {
                // 双指缩放
                const currentDistance = getTouchDistance(e);
                if (pinchStartDistance > 0) {
                    const scaleChange = currentDistance / pinchStartDistance;
                    const newScale = Math.max(0.1, Math.min(5, pinchStartScale * scaleChange));
                    
                    // 计算缩放中心（两指中点）
                    const rect = canvas.getBoundingClientRect();
                    const touch1 = e.touches[0];
                    const touch2 = e.touches[1];
                    const centerX = (touch1.clientX + touch2.clientX) / 2 - rect.left;
                    const centerY = (touch1.clientY + touch2.clientY) / 2 - rect.top;
                    
                    // 计算缩放中心在画布坐标系中的位置
                    const mouseX = (centerX - transform.x) / transform.scale;
                    const mouseY = (centerY - transform.y) / transform.scale;
                    
                    // 更新变换
                    transform.scale = newScale;
                    transform.x = centerX - mouseX * newScale;
                    transform.y = centerY - mouseY * newScale;
                    
                    drawScene();
                }
            }
        }
        
        // 触摸结束事件
        function handleTouchEnd(e) {
            e.preventDefault();
            
            touchCount = e.touches.length;
            
            if (touchCount === 0) {
                // 所有手指离开
                const currentTime = Date.now();
                const touchDuration = currentTime - touchStartTime;
                
                // 检查是否为长按
                if (touchDuration >= LONG_PRESS_DURATION && !isLongPressed && longPressTarget) {
                    const distance = Math.sqrt(
                        Math.pow(lastTouchPos.x - touchStartPos.x, 2) + 
                        Math.pow(lastTouchPos.y - touchStartPos.y, 2)
                    );
                    
                    if (distance <= LONG_PRESS_TOLERANCE) {
                        // 触发长按
                        isLongPressed = true;
                        handleLongPress(longPressTarget.type, longPressTarget.target);
                    }
                }
                

                
                // 清理状态
                clearLongPressTimer();
                isDragging = false;
                isVertexDragging = false;
                draggedVertex = null;
                
                // 如果正在绘画，结束当前路径
                if (isDrawing && currentPath) {
                    drawingPaths.push(currentPath);
                    currentPath = null;
                    isDrawing = false;
                    drawScene();
                }
                
                // 如果正在擦除，结束擦除
                if (isErasing) {
                    isErasing = false;
                    drawScene();
                }
                
                // 重置长按状态（延迟重置避免与双击冲突）
                setTimeout(() => {
                    isLongPressed = false;
                    longPressTarget = null;
                }, 50);
                
                // 重置缩放相关状态
                pinchStartDistance = 0;
                pinchStartScale = 1;
            }
        }
        
        // 触摸双击事件
        function handleTouchDoubleClick(pos) {
            // 转换为画布坐标
            const canvasPos = screenToCanvas(pos.clientX, pos.clientY);
            
            // 检查是否双击在顶点上
            const clickedVertex = getClickedVertex(canvasPos.x, canvasPos.y);
            if (clickedVertex) {
                toggleAngleLock(clickedVertex);
                return;
            }
            
            // 检查是否双击在边上
            const clickedEdge = getClickedEdge(canvasPos.x, canvasPos.y);
            if (clickedEdge) {
                toggleEdgeLock(clickedEdge);
                return;
            }
        }
        
        // 鼠标按下事件
        function handleMouseDown(e) {
            const rect = canvas.getBoundingClientRect();
            const clientX = e.clientX - rect.left;
            const clientY = e.clientY - rect.top;
            
            // 转换为画布坐标
            const canvasPos = screenToCanvas(clientX, clientY);
            
            // 如果处于绘画模式，开始绘画（不检测顶点或边）
            if (drawingMode) {
                if (eraserMode) {
                    // 橡皮擦模式
                    isErasing = true;
                    eraseAtPosition(canvasPos.x, canvasPos.y);
                    canvas.style.cursor = 'crosshair';
                } else {
                    // 画笔模式
                    isDrawing = true;
                    currentPath = {
                        points: [{ x: canvasPos.x, y: canvasPos.y }],
                        color: brushColor,
                        size: brushSize
                    };
                    canvas.style.cursor = 'crosshair';
                }
                
                // 画笔模式下不处理顶点或边的交互
                return;
            }
            
            // 重置长按状态
            isLongPressed = false;
            clearLongPressTimer();
            
            // 检查是否点击在顶点上
            const clickedVertex = getClickedVertex(canvasPos.x, canvasPos.y);
            
            if (clickedVertex) {
                // 开始长按检测
                startLongPress('vertex', clickedVertex, clientX, clientY);
                
                // 准备拖拽顶点
                draggedVertex = clickedVertex;
                canvas.style.cursor = 'grabbing';
            } else {
                // 检查是否点击在边上
                const clickedEdge = getClickedEdge(canvasPos.x, canvasPos.y);
                
                if (clickedEdge) {
                    // 开始长按检测
                    startLongPress('edge', clickedEdge, clientX, clientY);
                } else {
                    // 开始拖拽画布
                    isDragging = true;
                    dragStartPos = { x: clientX, y: clientY };
                    canvas.style.cursor = 'grabbing';
                }
            }
        }
        
        // 鼠标移动事件
        function handleMouseMove(e) {
            const rect = canvas.getBoundingClientRect();
            const clientX = e.clientX - rect.left;
            const clientY = e.clientY - rect.top;
            
            // 转换为画布坐标
            const canvasPos = screenToCanvas(clientX, clientY);
            
            // 更新鼠标位置（用于橡皮擦预览）
            mousePos = canvasPos;
            
            // 如果处于橡皮擦模式且在画笔模式下，实时更新预览
            if (eraserMode && drawingMode && !isErasing) {
                drawScene();
            }
            
            // 如果正在绘画，添加点到当前路径
            if (isDrawing && currentPath) {
                currentPath.points.push({ x: canvasPos.x, y: canvasPos.y });
                drawScene();
                return;
            }
            
            // 如果正在擦除，继续擦除
            if (isErasing) {
                eraseAtPosition(canvasPos.x, canvasPos.y);
                return;
            }
            
            // 检查长按期间是否移动过多
            if (longPressTimer && !isLongPressed) {
                const dx = clientX - longPressStartPos.x;
                const dy = clientY - longPressStartPos.y;
                const distance = Math.sqrt(dx * dx + dy * dy);
                
                if (distance > LONG_PRESS_TOLERANCE) {
                    // 移动距离过大，取消长按，开始拖拽
                    clearLongPressTimer();
                    if (longPressTarget && longPressTarget.type === 'vertex') {
                        isVertexDragging = true;
                    }
                }
            }
            
            if (isVertexDragging && draggedVertex && !isLongPressed) {
                // 特殊逻辑：AAA情况下任何顶点都可以缩放
                if (canPerformAAAScaling()) {
                    scaleTriangleProportionally(draggedVertex, canvasPos);
                } 
                // 两角固定且可以缩放（非ASA情况），拖拽第三个顶点时进行等比缩放
                else if (canPerformTwoAngleScaling() && draggedVertex === getUnfixedAngle()) {
                    scaleTriangleProportionally(draggedVertex, canvasPos);
                } else if (fixedAngles[draggedVertex]) {
                    // 如果拖拽的顶点角度被固定，则拖拽整个三角形而不是单个顶点
                    const dx = canvasPos.x - triangle[draggedVertex].x;
                    const dy = canvasPos.y - triangle[draggedVertex].y;
                    
                    // 移动整个三角形
                    triangle.A.x += dx;
                    triangle.A.y += dy;
                    triangle.B.x += dx;
                    triangle.B.y += dy;
                    triangle.C.x += dx;
                    triangle.C.y += dy;
                } else {
                    // 普通拖拽顶点
                    // 应用约束
                    applyConstraints(draggedVertex, canvasPos);
                }
                
                drawScene();
                updateTriangleInfo();
                updateConditionDisplay();
            } else if (isDragging) {
                // 拖拽画布
                const dx = clientX - dragStartPos.x;
                const dy = clientY - dragStartPos.y;
                
                transform.x += dx;
                transform.y += dy;
                
                dragStartPos = { x: clientX, y: clientY };
                drawScene();
            } else if (!longPressTimer && !isLongPressed && !drawingMode) {
                // 更新鼠标样式（只在没有长按时且不在绘画模式）
                const clickedVertex = getClickedVertex(canvasPos.x, canvasPos.y);
                const clickedEdge = getClickedEdge(canvasPos.x, canvasPos.y);
                
                if (clickedVertex || clickedEdge) {
                    canvas.style.cursor = 'pointer';
                } else {
                    canvas.style.cursor = 'grab';
                }
            } else if (drawingMode && !isDrawing) {
                // 绘画模式下的鼠标样式
                canvas.style.cursor = 'crosshair';
            }
        }
        
        // 鼠标离开事件
        function handleMouseLeave() {
            // 清除鼠标位置
            mousePos = null;
            
            // 如果处于橡皮擦模式，重新绘制以清除预览
            if (eraserMode && drawingMode) {
                drawScene();
            }
            
            // 调用鼠标抬起事件处理
            handleMouseUp();
        }
        
        // 鼠标抬起事件
        function handleMouseUp() {
            // 如果正在绘画，结束当前路径
            if (isDrawing && currentPath) {
                drawingPaths.push(currentPath);
                currentPath = null;
                isDrawing = false;
                drawScene();
            }
            
            // 如果正在擦除，结束擦除
            if (isErasing) {
                isErasing = false;
                drawScene();
            }
            
            // 清除长按定时器
            clearLongPressTimer();
            
            // 重置拖拽状态
            isDragging = false;
            isVertexDragging = false;
            draggedVertex = null;
            
            // 重置长按状态
            setTimeout(() => {
                isLongPressed = false;
                longPressTarget = null;
            }, 50); // 短暂延迟避免与双击冲突
            
            // 设置合适的鼠标样式
            if (drawingMode) {
                canvas.style.cursor = 'crosshair';
            } else {
                canvas.style.cursor = 'grab';
            }
        }
        
        // 滚轮缩放事件
        function handleWheel(e) {
            e.preventDefault();
            
            const rect = canvas.getBoundingClientRect();
            const clientX = e.clientX - rect.left;
            const clientY = e.clientY - rect.top;
            
            // 缩放因子
            const scaleFactor = e.deltaY > 0 ? 0.9 : 1.1;
            const newScale = Math.max(0.1, Math.min(5, transform.scale * scaleFactor));
            
            // 计算缩放中心
            const mouseX = (clientX - transform.x) / transform.scale;
            const mouseY = (clientY - transform.y) / transform.scale;
            
            // 更新变换
            transform.scale = newScale;
            transform.x = clientX - mouseX * newScale;
            transform.y = clientY - mouseY * newScale;
            
            drawScene();
        }
        
        // 双击事件
        function handleDoubleClick(e) {
            // 如果刚刚长按过，忽略双击
            if (isLongPressed) {
                return;
            }
            
            const rect = canvas.getBoundingClientRect();
            const clientX = e.clientX - rect.left;
            const clientY = e.clientY - rect.top;
            
            // 转换为画布坐标
            const canvasPos = screenToCanvas(clientX, clientY);
            
            // 检查是否双击在顶点上
            const clickedVertex = getClickedVertex(canvasPos.x, canvasPos.y);
            if (clickedVertex) {
                toggleAngleLock(clickedVertex);
                return;
            }
            
            // 检查是否双击在边上
            const clickedEdge = getClickedEdge(canvasPos.x, canvasPos.y);
            if (clickedEdge) {
                toggleEdgeLock(clickedEdge);
                return;
            }
        }
        
        // 开始长按检测
        function startLongPress(type, target, clientX, clientY) {
            longPressTarget = { type, target };
            longPressStartPos = { x: clientX, y: clientY };
            
            console.log(`开始长按检测: ${type} - ${target}`, { x: clientX, y: clientY });
            
            longPressTimer = setTimeout(() => {
                // 长按触发
                isLongPressed = true;
                console.log(`长按定时器触发: ${type} - ${target}`);
                handleLongPress(type, target);
                
                // 清除定时器
                longPressTimer = null;
            }, LONG_PRESS_DURATION);
        }
        
        // 清除长按定时器
        function clearLongPressTimer() {
            if (longPressTimer) {
                clearTimeout(longPressTimer);
                longPressTimer = null;
            }
        }
        
        // 处理长按事件
        function handleLongPress(type, target) {
            console.log(`长按事件处理: ${type} - ${target}`);
            
            if (type === 'vertex') {
                // 长按顶点，切换角度锁定
                console.log(`切换角度锁定: ${target}`);
                toggleAngleLock(target);
                
                // 添加视觉反馈
                showLongPressEffect('角度固定状态已切换');
            } else if (type === 'edge') {
                // 长按边，切换边长锁定
                console.log(`切换边长锁定: ${target}`);
                toggleEdgeLock(target);
                
                // 添加视觉反馈
                showLongPressEffect('边长固定状态已切换');
            }
        }
        
        // 显示长按反馈效果
        function showLongPressEffect(message) {
            // 创建临时提示元素
            const feedback = document.createElement('div');
            feedback.textContent = message;
            feedback.style.cssText = `
                position: fixed;
                top: 50%;
                left: 50%;
                transform: translate(-50%, -50%);
                background: rgba(79, 172, 254, 0.9);
                color: white;
                padding: 10px 20px;
                border-radius: 20px;
                font-size: 14px;
                font-weight: bold;
                z-index: 1000;
                pointer-events: none;
                animation: longPressFeedback 1.5s ease-out forwards;
            `;
            
            // 添加CSS动画
            if (!document.getElementById('longPressStyle')) {
                const style = document.createElement('style');
                style.id = 'longPressStyle';
                style.textContent = `
                    @keyframes longPressFeedback {
                        0% { opacity: 0; transform: translate(-50%, -50%) scale(0.8); }
                        20% { opacity: 1; transform: translate(-50%, -50%) scale(1); }
                        80% { opacity: 1; transform: translate(-50%, -50%) scale(1); }
                        100% { opacity: 0; transform: translate(-50%, -50%) scale(0.8); }
                    }
                `;
                document.head.appendChild(style);
            }
            
            document.body.appendChild(feedback);
            
            // 1.5秒后移除
            setTimeout(() => {
                if (feedback.parentNode) {
                    feedback.parentNode.removeChild(feedback);
                }
            }, 1500);
        }
        
        // 切换角度锁定
        function toggleAngleLock(vertex) {
            // 检查是否超过最大固定数量限制
            if (!fixedAngles[vertex] && getTotalFixedCount() >= 3) {
                showMaxLimitMessage();
                return;
            }
            
            fixedAngles[vertex] = !fixedAngles[vertex];
            
            if (fixedAngles[vertex]) {
                // 记录当前角度
                initialAngles[vertex] = calculateAngle(
                    triangle[vertex], 
                    triangle[getOtherVertices(vertex)[0]], 
                    triangle[getOtherVertices(vertex)[1]]
                );
            } else {
                // 清除记录的角度
                delete initialAngles[vertex];
            }
            
            // 清除判定结果显示状态
            currentJudgeResult = null;
            judgeResultCondition = null;
            
            // 清除持久约束显示（因为约束已改变）
            persistentConstraints = null;
            persistentDraggedVertex = null;
            
            drawScene();
            updateTriangleInfo();
            updateConditionDisplay();
        }
        
        // 切换边长锁定
        function toggleEdgeLock(edge) {
            // 检查是否超过最大固定数量限制
            if (!fixedEdges[edge] && getTotalFixedCount() >= 3) {
                showMaxLimitMessage();
                return;
            }
            
            fixedEdges[edge] = !fixedEdges[edge];
            
            if (fixedEdges[edge]) {
                // 记录当前边长
                const vertices = getEdgeVertices(edge);
                initialEdgeLengths[edge] = distance(triangle[vertices[0]], triangle[vertices[1]]);
            } else {
                // 清除记录的边长
                delete initialEdgeLengths[edge];
            }
            
            // 清除判定结果显示状态
            currentJudgeResult = null;
            judgeResultCondition = null;
            
            // 清除持久约束显示（因为约束已改变）
            persistentConstraints = null;
            persistentDraggedVertex = null;
            
            drawScene();
            updateTriangleInfo();
            updateConditionDisplay();
        }
        
        // 获取其他两个顶点
        function getOtherVertices(vertex) {
            const vertices = ['A', 'B', 'C'];
            return vertices.filter(v => v !== vertex);
        }
        
        // 获取边对应的顶点
        function getEdgeVertices(edge) {
            switch (edge) {
                case 'a': return ['B', 'C']; // BC边
                case 'b': return ['A', 'C']; // AC边
                case 'c': return ['A', 'B']; // AB边
            }
        }
        
        // 屏幕坐标转画布坐标
        function screenToCanvas(screenX, screenY) {
            return {
                x: (screenX - transform.x) / transform.scale,
                y: (screenY - transform.y) / transform.scale
            };
        }
        
        // 画布坐标转屏幕坐标
        function canvasToScreen(canvasX, canvasY) {
            return {
                x: canvasX * transform.scale + transform.x,
                y: canvasY * transform.scale + transform.y
            };
        }
        
        // 检查点击的顶点
        function getClickedVertex(x, y) {
            // 为触屏设备增加更大的点击容忍度
            const baseTolerance = ('ontouchstart' in window) ? 35 : 20;
            const tolerance = baseTolerance / transform.scale; // 随缩放调整点击容忍度
            
            for (const [vertex, pos] of Object.entries(triangle)) {
                const distance = Math.sqrt((x - pos.x) ** 2 + (y - pos.y) ** 2);
                if (distance < tolerance) {
                    return vertex;
                }
            }
            return null;
        }
        
        // 检查点击的边
        function getClickedEdge(x, y) {
            // 为触屏设备增加更大的点击容忍度
            const baseTolerance = ('ontouchstart' in window) ? 25 : 15;
            const tolerance = baseTolerance / transform.scale;
            
            // 检查边a (BC)
            if (pointToLineDistance(x, y, triangle.B.x, triangle.B.y, triangle.C.x, triangle.C.y) < tolerance) {
                return 'a';
            }
            
            // 检查边b (AC) 
            if (pointToLineDistance(x, y, triangle.A.x, triangle.A.y, triangle.C.x, triangle.C.y) < tolerance) {
                return 'b';
            }
            
            // 检查边c (AB)
            if (pointToLineDistance(x, y, triangle.A.x, triangle.A.y, triangle.B.x, triangle.B.y) < tolerance) {
                return 'c';
            }
            
            return null;
        }
        
        // 计算点到线段的距离
        function pointToLineDistance(px, py, x1, y1, x2, y2) {
            const A = px - x1;
            const B = py - y1;
            const C = x2 - x1;
            const D = y2 - y1;
            
            const dot = A * C + B * D;
            const lenSq = C * C + D * D;
            
            if (lenSq === 0) return Math.sqrt(A * A + B * B);
            
            let param = dot / lenSq;
            
            let xx, yy;
            
            if (param < 0) {
                xx = x1;
                yy = y1;
            } else if (param > 1) {
                xx = x2;
                yy = y2;
            } else {
                xx = x1 + param * C;
                yy = y1 + param * D;
            }
            
            const dx = px - xx;
            const dy = py - yy;
            return Math.sqrt(dx * dx + dy * dy);
        }
        
        // 应用约束
        function applyConstraints(draggedVertex, newPos) {
            // 保存当前状态
            const backup = {
                A: { ...triangle.A },
                B: { ...triangle.B },
                C: { ...triangle.C }
            };
            
            // 应用精确的几何约束
            const constrainedPos = applyGeometricConstraints(draggedVertex, newPos);
            
            if (constrainedPos) {
                // 使用约束后的位置
                triangle[draggedVertex] = constrainedPos;
                
                // 应用其他约束（智能策略）
                const success = applyConstraintsSmartly(draggedVertex);
                
                // 如果约束应用失败，恢复原状态
                if (!success) {
                    triangle.A = backup.A;
                    triangle.B = backup.B;
                    triangle.C = backup.C;
                }
            } else {
                // 如果无法找到合适的约束位置，恢复原状态
                triangle.A = backup.A;
                triangle.B = backup.B;
                triangle.C = backup.C;
            }
        }
        
        // 智能应用约束
        function applyConstraintsSmartly(draggedVertex) {
            const maxIterations = 10;
            let iteration = 0;
            
            while (iteration < maxIterations) {
                let constraintViolated = false;
                
                // 应用边长约束
                constraintViolated = applyEdgeConstraintsSmartly(draggedVertex) || constraintViolated;
                
                // 应用角度约束
                constraintViolated = applyAngleConstraintsSmartly(draggedVertex) || constraintViolated;
                
                // 如果没有约束被违反，说明收敛了
                if (!constraintViolated) {
                    return true;
                }
                
                iteration++;
            }
            
            // 达到最大迭代次数，约束应用失败
            return false;
        }
        
        // 智能应用边长约束
        function applyEdgeConstraintsSmartly(draggedVertex) {
            let anyConstraintApplied = false;
            
            for (const [edge, isFixed] of Object.entries(fixedEdges)) {
                if (!isFixed) continue;
                
                const vertices = getEdgeVertices(edge);
                const targetLength = initialEdgeLengths[edge];
                const currentLength = distance(triangle[vertices[0]], triangle[vertices[1]]);
                
                // 检查是否需要调整
                if (Math.abs(currentLength - targetLength) > 1.0) {
                    // 确定调整策略
                    if (vertices.includes(draggedVertex)) {
                        // 拖拽的顶点在这条边上，调整另一个顶点
                        const otherVertex = vertices.find(v => v !== draggedVertex);
                        adjustVertexToMaintainEdge(draggedVertex, otherVertex, targetLength);
                    } else {
                        // 拖拽的顶点不在这条边上，按比例调整两个顶点
                        adjustEdgeLength(vertices[0], vertices[1], targetLength);
                    }
                    anyConstraintApplied = true;
                }
            }
            
            return anyConstraintApplied;
        }
        
        // 智能应用角度约束
        function applyAngleConstraintsSmartly(draggedVertex) {
            let anyConstraintApplied = false;
            
            for (const [vertex, isFixed] of Object.entries(fixedAngles)) {
                if (!isFixed) continue;
                
                const targetAngle = initialAngles[vertex];
                const currentAngle = calculateAngle(
                    triangle[vertex], 
                    triangle[getOtherVertices(vertex)[0]], 
                    triangle[getOtherVertices(vertex)[1]]
                );
                
                // 检查是否需要调整
                if (Math.abs(currentAngle - targetAngle) > 1.0) {
                    // 智能调整角度
                    if (maintainAngleSmartly(vertex, targetAngle, draggedVertex)) {
                        anyConstraintApplied = true;
                    }
                }
            }
            
            return anyConstraintApplied;
        }
        
        // 调整顶点以保持边长
        function adjustVertexToMaintainEdge(fixedVertex, adjustVertex, targetLength) {
            const direction = {
                x: triangle[adjustVertex].x - triangle[fixedVertex].x,
                y: triangle[adjustVertex].y - triangle[fixedVertex].y
            };
            
            const currentLength = Math.sqrt(direction.x * direction.x + direction.y * direction.y);
            if (currentLength < 0.1) return;
            
            const scale = targetLength / currentLength;
            triangle[adjustVertex] = {
                x: triangle[fixedVertex].x + direction.x * scale,
                y: triangle[fixedVertex].y + direction.y * scale
            };
        }
        
        // 调整边长（等比例调整两个顶点）
        function adjustEdgeLength(v1, v2, targetLength) {
            const midX = (triangle[v1].x + triangle[v2].x) / 2;
            const midY = (triangle[v1].y + triangle[v2].y) / 2;
            
            const direction = {
                x: triangle[v2].x - triangle[v1].x,
                y: triangle[v2].y - triangle[v1].y
            };
            
            const currentLength = Math.sqrt(direction.x * direction.x + direction.y * direction.y);
            if (currentLength < 0.1) return;
            
            const scale = targetLength / currentLength;
            const halfDirection = {
                x: direction.x * scale / 2,
                y: direction.y * scale / 2
            };
            
            triangle[v1] = {
                x: midX - halfDirection.x,
                y: midY - halfDirection.y
            };
            triangle[v2] = {
                x: midX + halfDirection.x,
                y: midY + halfDirection.y
            };
        }
        
        // 智能保持角度
        function maintainAngleSmartly(vertex, targetAngle, draggedVertex) {
            const otherVertices = getOtherVertices(vertex);
            const [v1, v2] = otherVertices;
            
            // 确定调整策略
            if (draggedVertex === vertex) {
                // 拖拽的是角的顶点，不调整其他顶点
                return false;
            } else if (draggedVertex === v1) {
                // 拖拽的是v1，调整v2以保持角度
                return adjustVertexToMaintainAngle(vertex, v1, v2, targetAngle);
            } else if (draggedVertex === v2) {
                // 拖拽的是v2，调整v1以保持角度
                return adjustVertexToMaintainAngle(vertex, v2, v1, targetAngle);
            } else {
                // 拖拽的是第三个顶点，选择一个顶点调整
                return adjustVertexToMaintainAngle(vertex, v1, v2, targetAngle);
            }
        }
        
        // 调整顶点以保持角度
        function adjustVertexToMaintainAngle(vertex, fixedVertex, adjustVertex, targetAngle) {
            // 保存当前adjustVertex的位置，用于选择最近的解
            const currentAdjustPos = { ...triangle[adjustVertex] };
            
            // 计算从vertex到fixedVertex的向量
            const vec1 = {
                x: triangle[fixedVertex].x - triangle[vertex].x,
                y: triangle[fixedVertex].y - triangle[vertex].y
            };
            
            const len1 = Math.sqrt(vec1.x * vec1.x + vec1.y * vec1.y);
            if (len1 < 0.1) return false;
            
            const unitVec1 = {
                x: vec1.x / len1,
                y: vec1.y / len1
            };
            
            // 计算目标长度
            const len2 = distance(triangle[vertex], triangle[adjustVertex]);
            
            // 计算目标角度对应的两个可能方向
            const angleRad = targetAngle * Math.PI / 180;
            const cos = Math.cos(angleRad);
            const sin = Math.sin(angleRad);
            
            // 方向1：逆时针旋转
            const unitVec2_ccw = {
                x: unitVec1.x * cos - unitVec1.y * sin,
                y: unitVec1.x * sin + unitVec1.y * cos
            };
            
            // 方向2：顺时针旋转（负角度）
            const unitVec2_cw = {
                x: unitVec1.x * cos + unitVec1.y * sin,
                y: -unitVec1.x * sin + unitVec1.y * cos
            };
            
            // 计算两个可能的新位置
            const newPos1 = {
                x: triangle[vertex].x + unitVec2_ccw.x * len2,
                y: triangle[vertex].y + unitVec2_ccw.y * len2
            };
            
            const newPos2 = {
                x: triangle[vertex].x + unitVec2_cw.x * len2,
                y: triangle[vertex].y + unitVec2_cw.y * len2
            };
            
            // 计算哪个位置离当前位置更近
            const dist1 = Math.sqrt(
                (newPos1.x - currentAdjustPos.x) ** 2 + 
                (newPos1.y - currentAdjustPos.y) ** 2
            );
            
            const dist2 = Math.sqrt(
                (newPos2.x - currentAdjustPos.x) ** 2 + 
                (newPos2.y - currentAdjustPos.y) ** 2
            );
            
            // 选择距离更近的位置
            triangle[adjustVertex] = dist1 <= dist2 ? newPos1 : newPos2;
            
            return true;
        }
        
        // 创建等腰三角形
        function createEquilateralTriangle() {
            // 使用更大的基准尺寸，并基于画布大小动态调整
            const canvasSize = Math.min(canvas.width, canvas.height);
            const baseSize = canvasSize * 0.6; // 使用画布尺寸的60%作为基准
            
            // 画布中心点（不受变换影响的逻辑坐标）
            const centerX = canvas.width / 2 - canvas.width * 0.05;  // 向左偏移5%
            const centerY = canvas.height / 2 + canvas.height * 0.02; // 向下偏移2%
            
            // 等腰三角形参数（确保精确的几何关系）
            const baseLength = baseSize * 0.8; // 底边长度
            const sideLength = baseSize * 0.7; // 两腰长度（相等）
            
            // 根据等腰三角形的几何关系计算高度
            // h = sqrt(sideLength^2 - (baseLength/2)^2)
            const height = Math.sqrt(sideLength * sideLength - (baseLength / 2) * (baseLength / 2));
            
            // 计算三角形重心（距离底边高度的1/3处）
            const centroidHeight = height / 3;
            
            // 计算三个顶点的坐标，使重心位于画布中心
            const A = {
                x: centerX,                           // 顶点A在顶部中央
                y: centerY - centroidHeight * 2      // 顶点A在重心上方2/3高度处
            };
            
            const B = {
                x: centerX - baseLength / 2,         // 底边左端点
                y: centerY + centroidHeight          // 底边在重心下方1/3高度处
            };
            
            const C = {
                x: centerX + baseLength / 2,         // 底边右端点
                y: centerY + centroidHeight          // 底边在重心下方1/3高度处
            };
            
            triangle = { A, B, C };
            
            // 验证三角形属性（调试用）
            const actualSideA = distance(triangle.B, triangle.C);
            const actualSideB = distance(triangle.A, triangle.C);
            const actualSideC = distance(triangle.A, triangle.B);
            
            console.log('初始化等腰三角形:');
            console.log('画布尺寸:', canvas.width, 'x', canvas.height);
            console.log('设计参数:');
            console.log('  底边长度:', baseLength.toFixed(1));
            console.log('  腰长:', sideLength.toFixed(1));
            console.log('  高度:', height.toFixed(1));
            console.log('实际测量:');
            console.log('  边a(BC):', actualSideA.toFixed(1));
            console.log('  边b(AC):', actualSideB.toFixed(1));
            console.log('  边c(AB):', actualSideC.toFixed(1));
            console.log('等腰验证:', Math.abs(actualSideB - actualSideC) < 0.1 ? '✓ 腰长相等' : '✗ 腰长不等');
            
            // 更新信息显示
            updateTriangleInfo();
        }
        
        // 更新三角形信息
        function updateTriangleInfo() {
            if (!triangle) return;
            
            // 计算边长（像素）
            const sideA_px = distance(triangle.B, triangle.C);
            const sideB_px = distance(triangle.A, triangle.C);
            const sideC_px = distance(triangle.A, triangle.B);
            
            // 转换为厘米（100像素 = 1厘米）
            const sideA_cm = sideA_px / 100;
            const sideB_cm = sideB_px / 100;
            const sideC_cm = sideC_px / 100;
            
            // 计算角度
            let angleA = calculateAngle(triangle.A, triangle.B, triangle.C);
            let angleB = calculateAngle(triangle.B, triangle.A, triangle.C);
            let angleC = calculateAngle(triangle.C, triangle.A, triangle.B);
            
            // 添加调试信息
            console.log('原始角度:', angleA.toFixed(3), angleB.toFixed(3), angleC.toFixed(3), '和:', (angleA + angleB + angleC).toFixed(3));
            
            // 确保角度和为180°（强制修正）
            // 先计算原始角度和
            const originalSum = angleA + angleB + angleC;
            
            // 如果角度和不是180，强制修正
            if (Math.abs(originalSum - 180) > 0.001) {
                // 计算需要修正的总量
                const totalCorrection = 180 - originalSum;
                
                // 按比例分配修正量（避免某个角度变化过大）
                const correctionA = (angleA / originalSum) * totalCorrection;
                const correctionB = (angleB / originalSum) * totalCorrection;
                const correctionC = (angleC / originalSum) * totalCorrection;
                
                angleA += correctionA;
                angleB += correctionB;
                angleC += correctionC;
                
                console.log('修正后角度:', angleA.toFixed(3), angleB.toFixed(3), angleC.toFixed(3), '和:', (angleA + angleB + angleC).toFixed(3));
            }
            
            // 最后四舍五入到一位小数
            angleA = Math.round(angleA * 10) / 10;
            angleB = Math.round(angleB * 10) / 10;
            angleC = Math.round(angleC * 10) / 10;
            
            // 最终检查：如果四舍五入后角度和不是180，微调最大角度
            const finalSum = angleA + angleB + angleC;
            if (finalSum !== 180) {
                const finalCorrection = 180 - finalSum;
                
                // 找到最大角度并微调
                if (angleA >= angleB && angleA >= angleC) {
                    angleA += finalCorrection;
                } else if (angleB >= angleA && angleB >= angleC) {
                    angleB += finalCorrection;
                } else {
                    angleC += finalCorrection;
                }
                
                console.log('最终角度:', angleA.toFixed(1), angleB.toFixed(1), angleC.toFixed(1), '和:', (angleA + angleB + angleC).toFixed(1));
            }
            
            // 最终显示前的强制校验
            const displaySum = angleA + angleB + angleC;
            console.log('显示前角度和:', displaySum.toFixed(1));
            
            // 如果显示的角度和不是180，强制调整显示值
            if (Math.abs(displaySum - 180) > 0.01) {
                const displayCorrection = (180 - displaySum) / 3;
                angleA += displayCorrection;
                angleB += displayCorrection;
                angleC += displayCorrection;
                console.log('显示值已强制修正为180°');
            }
            
            // 更新显示（边长显示为厘米）
            // 桌面版
            document.getElementById('sideA').textContent = sideA_cm.toFixed(1) + ' cm';
            document.getElementById('sideB').textContent = sideB_cm.toFixed(1) + ' cm';
            document.getElementById('sideC').textContent = sideC_cm.toFixed(1) + ' cm';
            document.getElementById('angleA').textContent = angleA.toFixed(1) + '°';
            document.getElementById('angleB').textContent = angleB.toFixed(1) + '°';
            document.getElementById('angleC').textContent = angleC.toFixed(1) + '°';
            
            // 移动端（如果存在）
            const mobileSideA = document.getElementById('mobile-sideA');
            const mobileSideB = document.getElementById('mobile-sideB');
            const mobileSideC = document.getElementById('mobile-sideC');
            const mobileAngleA = document.getElementById('mobile-angleA');
            const mobileAngleB = document.getElementById('mobile-angleB');
            const mobileAngleC = document.getElementById('mobile-angleC');
            
            if (mobileSideA) mobileSideA.textContent = sideA_cm.toFixed(1) + ' cm';
            if (mobileSideB) mobileSideB.textContent = sideB_cm.toFixed(1) + ' cm';
            if (mobileSideC) mobileSideC.textContent = sideC_cm.toFixed(1) + ' cm';
            if (mobileAngleA) mobileAngleA.textContent = angleA.toFixed(1) + '°';
            if (mobileAngleB) mobileAngleB.textContent = angleB.toFixed(1) + '°';
            if (mobileAngleC) mobileAngleC.textContent = angleC.toFixed(1) + '°';
            
            // 验证最终显示的角度和
            const finalDisplaySum = angleA + angleB + angleC;
            console.log('最终显示角度和:', finalDisplaySum.toFixed(1) + '°');
        }
        
        // 计算两点间距离
        function distance(p1, p2) {
            return Math.sqrt((p2.x - p1.x) ** 2 + (p2.y - p1.y) ** 2);
        }
        
        // 计算角度（度数）
        function calculateAngle(vertex, p1, p2) {
            const a = distance(p1, p2);
            const b = distance(vertex, p2);
            const c = distance(vertex, p1);
            
            const cosAngle = (b * b + c * c - a * a) / (2 * b * c);
            return Math.acos(Math.max(-1, Math.min(1, cosAngle))) * 180 / Math.PI;
        }
        
        // 绘制整个场景
        function drawScene() {
            // 保存上下文状态
            ctx.save();
            
            // 清除画布
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            
            // 应用变换
            ctx.translate(transform.x, transform.y);
            ctx.scale(transform.scale, transform.scale);
            
            // 绘制网格
            drawGrid();
            
            // 绘制三角形
            if (triangle) {
                drawTriangle();
            }
            
            // 绘制画笔路径
            drawBrushPaths();
            
            // 恢复上下文状态
            ctx.restore();
        }
        
        // 绘制背景网格
        function drawGrid() {
            ctx.setLineDash([]);
            
            // 小网格间距（25像素 = 0.25厘米）
            const smallGridSize = 25;
            // 大网格间距（100像素 = 1厘米）
            const largeGridSize = 100;
            
            // 计算可见区域
            const startX = Math.floor(-transform.x / transform.scale / smallGridSize) * smallGridSize;
            const endX = Math.ceil((canvas.width - transform.x) / transform.scale / smallGridSize) * smallGridSize;
            const startY = Math.floor(-transform.y / transform.scale / smallGridSize) * smallGridSize;
            const endY = Math.ceil((canvas.height - transform.y) / transform.scale / smallGridSize) * smallGridSize;
            
            // 绘制小网格线（0.25厘米间距）
            ctx.strokeStyle = 'rgba(100, 100, 140, 0.15)';
            ctx.lineWidth = 1 / transform.scale;
            
            // 绘制垂直小网格线
            for (let x = startX; x <= endX; x += smallGridSize) {
                if (x % largeGridSize !== 0) { // 不是大网格线的位置
                    ctx.beginPath();
                    ctx.moveTo(x, startY);
                    ctx.lineTo(x, endY);
                    ctx.stroke();
                }
            }
            
            // 绘制水平小网格线
            for (let y = startY; y <= endY; y += smallGridSize) {
                if (y % largeGridSize !== 0) { // 不是大网格线的位置
                    ctx.beginPath();
                    ctx.moveTo(startX, y);
                    ctx.lineTo(endX, y);
                    ctx.stroke();
                }
            }
            
            // 绘制大网格线（1厘米间距）
            ctx.strokeStyle = 'rgba(100, 100, 140, 0.3)';
            ctx.lineWidth = 2 / transform.scale;
            
            // 计算大网格的可见区域
            const startLargeX = Math.floor(-transform.x / transform.scale / largeGridSize) * largeGridSize;
            const endLargeX = Math.ceil((canvas.width - transform.x) / transform.scale / largeGridSize) * largeGridSize;
            const startLargeY = Math.floor(-transform.y / transform.scale / largeGridSize) * largeGridSize;
            const endLargeY = Math.ceil((canvas.height - transform.y) / transform.scale / largeGridSize) * largeGridSize;
            
            // 绘制垂直大网格线
            for (let x = startLargeX; x <= endLargeX; x += largeGridSize) {
                ctx.beginPath();
                ctx.moveTo(x, startLargeY);
                ctx.lineTo(x, endLargeY);
                ctx.stroke();
            }
            
            // 绘制水平大网格线
            for (let y = startLargeY; y <= endLargeY; y += largeGridSize) {
                ctx.beginPath();
                ctx.moveTo(startLargeX, y);
                ctx.lineTo(endLargeX, y);
                ctx.stroke();
            }
        }
        
        // 绘制画笔路径
        function drawBrushPaths() {
            // 绘制已完成的路径
            drawingPaths.forEach(path => {
                drawPath(path);
            });
            
            // 绘制当前正在绘制的路径
            if (currentPath && currentPath.points.length > 0) {
                drawPath(currentPath);
            }
        }
        
        // 绘制单个路径
        function drawPath(path) {
            if (!path || path.points.length < 2) return;
            
            ctx.save();
            ctx.strokeStyle = path.color;
            ctx.lineWidth = path.size / transform.scale;
            ctx.lineCap = 'round';
            ctx.lineJoin = 'round';
            ctx.setLineDash([]);
            
            ctx.beginPath();
            ctx.moveTo(path.points[0].x, path.points[0].y);
            
            for (let i = 1; i < path.points.length; i++) {
                ctx.lineTo(path.points[i].x, path.points[i].y);
            }
            
            ctx.stroke();
            ctx.restore();
        }

        
        // 绘制边
        function drawEdge(p1, p2, label) {
            ctx.beginPath();
            ctx.moveTo(p1.x, p1.y);
            ctx.lineTo(p2.x, p2.y);
            
            // 根据固定状态设置样式
            const isFixed = fixedEdges[label];
            if (isFixed) {
                // 固定的边：红色实线
                ctx.setLineDash([]);
                ctx.strokeStyle = '#ff4b2b';
                ctx.lineWidth = 4 / transform.scale;
            } else {
                // 普通的边：蓝色虚线
                ctx.setLineDash([8 / transform.scale, 4 / transform.scale]);
                ctx.strokeStyle = '#4facfe';
                ctx.lineWidth = 3 / transform.scale;
            }
            ctx.stroke();
            
            // 绘制边标签
            const midX = (p1.x + p2.x) / 2;
            const midY = (p1.y + p2.y) / 2;
            
            ctx.font = `bold ${16 / transform.scale}px Arial`;
            ctx.fillStyle = isFixed ? '#ff4b2b' : '#fff';
            ctx.textAlign = 'center';
            ctx.textBaseline = 'middle';
            ctx.setLineDash([]);
            
            // 直接绘制标签文字，无背景
            ctx.fillText(label, midX, midY);
        }
        
        // 绘制顶点
        function drawVertex(point, label, color) {
            const radius = 12 / transform.scale;
            const isAngleFixed = fixedAngles[label];
            
            // 如果角度被固定，先绘制红色外框
            if (isAngleFixed) {
                ctx.beginPath();
                ctx.arc(point.x, point.y, radius + 4 / transform.scale, 0, Math.PI * 2);
                ctx.strokeStyle = '#ff4b2b';
                ctx.lineWidth = 3 / transform.scale;
                ctx.setLineDash([]);
                ctx.stroke();
            }
            
            // 绘制顶点圆形
            ctx.beginPath();
            ctx.arc(point.x, point.y, radius, 0, Math.PI * 2);
            ctx.fillStyle = color;
            ctx.fill();
            
            // 绘制白色边框
            ctx.strokeStyle = '#fff';
            ctx.lineWidth = 2 / transform.scale;
            ctx.setLineDash([]);
            ctx.stroke();
            
            // 绘制顶点标签
            ctx.font = `bold ${18 / transform.scale}px Arial`;
            ctx.fillStyle = '#fff';
            ctx.textAlign = 'center';
            ctx.textBaseline = 'middle';
            ctx.fillText(label, point.x, point.y);
        }
        
        // 调整面板位置
        function adjustPanelPositions() {
            const conditionPanel = document.querySelector('.condition-panel');
            const historyPanel = document.querySelector('.history-panel');
            
            if (conditionPanel && historyPanel) {
                // 获取condition-panel的位置和高度
                const conditionRect = conditionPanel.getBoundingClientRect();
                const conditionBottom = conditionRect.bottom;
                const conditionRight = conditionRect.right;
                
                // 获取容器的位置，用于计算相对位置
                const container = document.querySelector('.canvas-container');
                const containerRect = container.getBoundingClientRect();
                
                // 计算history-panel应该的top位置（相对于容器）
                const newTop = conditionBottom - containerRect.top + 10; // condition-panel底部 + 10px间距
                
                // 设置history-panel的位置
                historyPanel.style.top = newTop + 'px';
            }
        }
        
        // 窗口大小改变时重新调整画布
        window.addEventListener('resize', function() {
            init();
        });
        
        // 初始化探索面板
        function initExplorationPanel() {
            // 加载历史探索记录
            loadExplorationHistory();
            
            // 添加桌面版事件监听
            document.getElementById('judge-button').addEventListener('click', handleJudgeClick);
            document.getElementById('reset-congruence').addEventListener('click', resetAllConstraints);
            document.getElementById('reset-triangle').addEventListener('click', resetTriangle);
            document.getElementById('summary-button').addEventListener('click', showSummaryModal);
            document.getElementById('restart-teaching').addEventListener('click', restartTeaching);
            
            // 添加移动端事件监听
            const mobileJudgeBtn = document.getElementById('mobile-judge-button');
            const mobileResetCongruence = document.getElementById('mobile-reset-congruence');
            const mobileResetTriangle = document.getElementById('mobile-reset-triangle');
            const mobileSummaryBtn = document.getElementById('mobile-summary-button');
            const mobileRestartBtn = document.getElementById('mobile-restart-teaching');
            
            if (mobileJudgeBtn) mobileJudgeBtn.addEventListener('click', handleJudgeClick);
            if (mobileResetCongruence) mobileResetCongruence.addEventListener('click', resetAllConstraints);
            if (mobileResetTriangle) mobileResetTriangle.addEventListener('click', resetTriangle);
            if (mobileSummaryBtn) mobileSummaryBtn.addEventListener('click', showSummaryModal);
            if (mobileRestartBtn) mobileRestartBtn.addEventListener('click', restartTeaching);
            
            // 添加模态框关闭事件监听
            document.getElementById('modal-close').addEventListener('click', closeSummaryModal);
            document.getElementById('summary-modal').addEventListener('click', function(e) {
                if (e.target === this) {
                    closeSummaryModal();
                }
            });
            
            // ESC键关闭模态框
            document.addEventListener('keydown', function(e) {
                if (e.key === 'Escape' && document.getElementById('summary-modal').style.display !== 'none') {
                    closeSummaryModal();
                }
            });
            
            // 初始状态更新
            updateConditionDisplay();
        }
        
        // 处理判定按钮点击
        function handleJudgeClick() {
            if (isJudging || !currentConditionString) return;
            
            // 防止快速重复点击
            const currentTime = Date.now();
            if (currentTime - lastJudgeTime < JUDGE_COOLDOWN) {
                console.log('判定冷却中，忽略快速点击');
                // 添加轻微的视觉反馈表示按钮在冷却
                const button = document.getElementById('judge-button');
                button.classList.add('cooldown');
                setTimeout(() => {
                    button.classList.remove('cooldown');
                }, 200);
                return;
            }
            
            // 检查是否重复（只在冷却时间外检查）
            if (successfulConditions.has(currentConditionString) || failedConditions.has(currentConditionString)) {
                // 更新最后判定时间，防止连续弹出重复提示
                lastJudgeTime = currentTime;
                showDuplicateMessage();
                return;
            }
            
            // 更新最后判定时间
            lastJudgeTime = currentTime;
            
            // 开始判定
            isJudging = true;
            document.getElementById('judge-button').disabled = true;
            
            // 执行判定逻辑
            const isSuccess = judgeCurrentCondition();
            
            // 显示结果动画
            setTimeout(() => {
                showJudgeResult(isSuccess);
                
                // 设置判定结果显示状态
                currentJudgeResult = isSuccess ? 'success' : 'failure';
                judgeResultCondition = currentConditionString;
                
                // 添加到历史记录
                if (isSuccess) {
                    successfulConditions.add(currentConditionString);
                } else {
                    failedConditions.add(currentConditionString);
                }
                
                // 保存到localStorage
                saveExplorationHistory();
                
                // 更新历史显示
                updateHistoryDisplay();
                
                // 立即重绘以显示判定结果样式
                drawScene();
                
                // 恢复按钮状态
                isJudging = false;
                document.getElementById('judge-button').disabled = false;
                
            }, 10); // 1.5秒的判定动画
        }
        
        // 重置所有约束
        function resetAllConstraints() {
            // 重置固定状态
            fixedAngles = { A: false, B: false, C: false };
            fixedEdges = { a: false, b: false, c: false };
            initialAngles = {};
            initialEdgeLengths = {};
            
            // 重置探索状态
            currentConditionString = '';
            isJudging = false;
            
            // 清除判定结果显示状态
            currentJudgeResult = null;
            judgeResultCondition = null;
            
            // 清除持久约束显示
            persistentConstraints = null;
            persistentDraggedVertex = null;
            
            // 清除所有画笔内容
            drawingPaths = [];
            currentPath = null;
            isDrawing = false;
            
            // 关闭画笔工具
            closeDrawingTool();
            
            // 更新显示
            updateConditionDisplay();
            drawScene();
        }
        
        // 重置三角形到初始状态
        function resetTriangle() {
            // 先重置所有约束
            resetAllConstraints();
            
            // 重新创建初始三角形
            createEquilateralTriangle();
            
            // 重置画布变换
            transform = {
                x: 0,
                y: 0,
                scale: 1
            };
            
            // 清除所有画笔内容
            drawingPaths = [];
            currentPath = null;
            isDrawing = false;
            
            // 关闭画笔工具
            closeDrawingTool();
            
            // 重新绘制
            drawScene();
            updateTriangleInfo();
        }
        
                 // 分析当前条件类型（基于几何关系）
         function analyzeConditionType() {
             const fixedEdgesList = Object.entries(fixedEdges).filter(([key, value]) => value).map(([key]) => key);
             const fixedAnglesList = Object.entries(fixedAngles).filter(([key, value]) => value).map(([key]) => key);
             
             const edgeCount = fixedEdgesList.length;
             const angleCount = fixedAnglesList.length;
             
             // 调试信息
             console.log('分析条件:', {
                 fixedEdges: fixedEdgesList,
                 fixedAngles: fixedAnglesList,
                 edgeCount,
                 angleCount
             });
             
             // SSS: 三边确定
             if (edgeCount === 3) {
                 console.log('判定为: SSS (三边确定)');
                 return 'SSS';
             }
             
             // AAA: 三角确定（但不能确定大小）
             if (angleCount === 3) {
                 console.log('判定为: AAA (三角确定)');
                 return 'AAA';
             }
             
             // 两边一角的情况
             if (edgeCount === 2 && angleCount === 1) {
                 const angle = fixedAnglesList[0];
                 const edges = fixedEdgesList;
                 
                 console.log(`检查两边一角: 角${angle}, 边[${edges.join(',')}]`);
                 
                 // 检查角是否是两边的夹角
                 if (isIncludedAngle(angle, edges)) {
                     console.log('判定为: SAS (边角边 - 两边夹着一个角)');
                     return 'SAS'; // 边角边：两边夹着一个角
                 } else {
                     console.log('判定为: SSA (边边角 - 两边不是夹角的两边)');
                     return 'SSA'; // 边边角：两边不是夹角的两边
                 }
             }
             
             // 两角一边的情况
             if (angleCount === 2 && edgeCount === 1) {
                 const edge = fixedEdgesList[0];
                 const angles = fixedAnglesList;
                 
                 console.log(`检查两角一边: 边${edge}, 角[${angles.join(',')}]`);
                 
                 // 检查边是否是两角的夹边
                 if (isIncludedEdge(edge, angles)) {
                     console.log('判定为: ASA (角边角 - 两个角夹着一条边)');
                     return 'ASA'; // 角边角：两个角夹着一条边
                 } else {
                     console.log('判定为: AAS (角角边 - 两个角和其中一个角的对边)');
                     return 'AAS'; // 角角边：两个角和其中一个角的对边
                 }
             }
             
             // 单一条件的情况
             if (edgeCount === 1 && angleCount === 0) {
                 console.log('判定为: S (单边)');
                 return 'S';
             }
             
             if (edgeCount === 0 && angleCount === 1) {
                 console.log('判定为: A (单角)');
                 return 'A';
             }
             
             // 两个条件的情况
             if (edgeCount === 2 && angleCount === 0) {
                 // 检查是否为直角三角形的HL情况
                 if (isRightTriangleHL(fixedEdgesList)) {
                     console.log('判定为: HL (斜边直角边)');
                     return 'HL';
                 } else {
                     console.log('判定为: SS (两边)');
                     return 'SS';
                 }
             }
             
             if (edgeCount === 0 && angleCount === 2) {
                 console.log('判定为: AA (两角)');
                 return 'AA';
             }
             
             if (edgeCount === 1 && angleCount === 1) {
                 const edge = fixedEdgesList[0];
                 const angle = fixedAnglesList[0];
                 
                 // 检查边和角的关系
                 const edgeAngleMap = {
                     'a': ['B', 'C'], // 边a(BC)对应角B和C
                     'b': ['A', 'C'], // 边b(AC)对应角A和C
                     'c': ['A', 'B']  // 边c(AB)对应角A和B
                 };
                 
                 const relatedAngles = edgeAngleMap[edge] || [];
                 if (relatedAngles.includes(angle)) {
                     console.log('判定为: SA (边角 - 边和其对应角)');
                     return 'SA';
                 } else {
                     console.log('判定为: AS (角边 - 角和非对应边)');
                     return 'AS';
                 }
             }
             
             // 没有固定条件的情况
             if (edgeCount === 0 && angleCount === 0) {
                 console.log('无固定条件');
                 return null;
             }
             
             // 其他情况（理论上不应该到达这里）
             console.log('未知条件组合');
             return null;
         }
        
        // 检查角是否为两边的夹角
        function isIncludedAngle(angle, edges) {
            const angleEdgeMap = {
                'A': ['b', 'c'], // 角A的夹边是b(AC)和c(AB)
                'B': ['a', 'c'], // 角B的夹边是a(BC)和c(AB)
                'C': ['a', 'b']  // 角C的夹边是a(BC)和b(AC)
            };
            
            const requiredEdges = angleEdgeMap[angle] || [];
            const isIncluded = edges.length === 2 && requiredEdges.every(edge => edges.includes(edge));
            
            console.log(`检查角${angle}是否为边[${edges.join(',')}]的夹角:`, {
                requiredEdges,
                actualEdges: edges,
                isIncluded
            });
            
            return isIncluded;
        }
        
        // 检查边是否为两角的夹边
        function isIncludedEdge(edge, angles) {
            const edgeAngleMap = {
                'a': ['B', 'C'], // 边a(BC)的夹角是B和C
                'b': ['A', 'C'], // 边b(AC)的夹角是A和C
                'c': ['A', 'B']  // 边c(AB)的夹角是A和B
            };
            
            const requiredAngles = edgeAngleMap[edge] || [];
            const isIncluded = angles.length === 2 && requiredAngles.every(angle => angles.includes(angle));
            
            console.log(`检查边${edge}是否为角[${angles.join(',')}]的夹边:`, {
                requiredAngles,
                actualAngles: angles,
                isIncluded
            });
            
            return isIncluded;
        }
        
        // 检查是否为直角三角形的HL情况（斜边+直角边）
        function isRightTriangleHL(fixedEdges) {
            if (fixedEdges.length !== 2) return false;
            
            // 首先检查是否有直角
            const rightAngle = findRightAngle();
            if (!rightAngle) return false;
            
            console.log(`发现直角: 角${rightAngle}`);
            
            // 获取直角对应的斜边和两条直角边
            const rightAngleInfo = {
                'A': { hypotenuse: 'a', legs: ['b', 'c'] }, // 角A是直角，斜边是a(BC)，直角边是b(AC)和c(AB)
                'B': { hypotenuse: 'b', legs: ['a', 'c'] }, // 角B是直角，斜边是b(AC)，直角边是a(BC)和c(AB)
                'C': { hypotenuse: 'c', legs: ['a', 'b'] }  // 角C是直角，斜边是c(AB)，直角边是a(BC)和b(AC)
            };
            
            const info = rightAngleInfo[rightAngle];
            if (!info) return false;
            
            // 检查固定的两条边是否包含斜边和一条直角边
            const hasHypotenuse = fixedEdges.includes(info.hypotenuse);
            const hasLeg = info.legs.some(leg => fixedEdges.includes(leg));
            
            const isHL = hasHypotenuse && hasLeg;
            
            console.log(`HL检查:`, {
                rightAngle,
                hypotenuse: info.hypotenuse,
                legs: info.legs,
                fixedEdges,
                hasHypotenuse,
                hasLeg,
                isHL
            });
            
            return isHL;
        }
        
        // 寻找直角（90度角）
        function findRightAngle() {
            if (!triangle) return null;
            
            const tolerance = 2; // 容忍度为2度
            
            // 计算三个角度
            const angleA = calculateAngle(triangle.A, triangle.B, triangle.C);
            const angleB = calculateAngle(triangle.B, triangle.A, triangle.C);
            const angleC = calculateAngle(triangle.C, triangle.A, triangle.B);
            
            console.log(`角度检查: A=${angleA.toFixed(1)}°, B=${angleB.toFixed(1)}°, C=${angleC.toFixed(1)}°`);
            
            // 检查哪个角接近90度
            if (Math.abs(angleA - 90) < tolerance) return 'A';
            if (Math.abs(angleB - 90) < tolerance) return 'B';
            if (Math.abs(angleC - 90) < tolerance) return 'C';
            
            return null;
        }
        
        // 判定当前条件是否能确定三角形（基于几何关系）
        function judgeCurrentCondition() {
            const conditionType = currentConditionString;
            
                         // 根据几何关系判定
             switch (conditionType) {
                 case 'SSS': // 三边确定
                 case 'SAS': // 边角边：两边夹着一个角
                 case 'ASA': // 角边角：两个角夹着一条边  
                 case 'AAS': // 角角边：两个角和其中一个角的对边
                 case 'HL':  // 斜边直角边（直角三角形专用）
                     return true;
                 
                 case 'SSA': // 边边角：两边不是夹角的两边
                 case 'S':   // 单边
                 case 'A':   // 单角
                 case 'SS':  // 两边
                 case 'AA':  // 两角
                 case 'AAA': // 三角
                 case 'SA':  // 边角（边和其对应角）
                 case 'AS':  // 角边（角和非对应边）
                     return false;
                 
                 // 其他未知组合
                 default:
                     return false;
             }
        }
        
        // 更新条件显示（基于几何关系）
        function updateConditionDisplay() {
            // 获取桌面版和移动端元素
            const conditionDisplay = document.getElementById('condition-display');
            const judgeButton = document.getElementById('judge-button');
            const mobileConditionDisplay = document.getElementById('mobile-condition-display');
            const mobileJudgeButton = document.getElementById('mobile-judge-button');
            
            // 分析条件类型
            const newConditionString = analyzeConditionType();
             
            // 如果条件发生变化，清除判定结果状态
            if (newConditionString !== currentConditionString) {
                currentJudgeResult = null;
                judgeResultCondition = null;
            }
             
            currentConditionString = newConditionString;
             
            if (currentConditionString && currentConditionString !== 'null') {
                // 获取固定的元素列表
                const fixedEdgesList = Object.entries(fixedEdges).filter(([key, value]) => value);
                const fixedAnglesList = Object.entries(fixedAngles).filter(([key, value]) => value);
                
                // 构建显示内容
                const displayContent = buildConditionDisplayContent(fixedEdgesList, fixedAnglesList);
                const buttonText = `🔍 判定 "${currentConditionString}" 是否能确定唯一三角形`;
                
                // 更新桌面版
                conditionDisplay.innerHTML = displayContent;
                judgeButton.disabled = false;
                judgeButton.textContent = buttonText;
                
                // 更新移动端
                if (mobileConditionDisplay) {
                    mobileConditionDisplay.innerHTML = displayContent;
                }
                if (mobileJudgeButton) {
                    mobileJudgeButton.disabled = false;
                    mobileJudgeButton.textContent = buttonText;
                }
                
            } else {
                // 显示空状态
                const emptyContent = '<span class="no-condition">尚未固定任何条件</span>';
                const emptyButtonText = '🔍 请先固定至少一个条件';
                
                // 更新桌面版
                conditionDisplay.innerHTML = emptyContent;
                judgeButton.disabled = true;
                judgeButton.textContent = emptyButtonText;
                
                // 更新移动端
                if (mobileConditionDisplay) {
                    mobileConditionDisplay.innerHTML = emptyContent;
                }
                if (mobileJudgeButton) {
                    mobileJudgeButton.disabled = true;
                    mobileJudgeButton.textContent = emptyButtonText;
                }
                
                currentConditionString = null;
            }
             
            // 延迟调整面板位置，确保DOM更新完成
            setTimeout(() => {
                adjustPanelPositions();
            }, 10);
        }
        
        // 构建条件显示内容
        function buildConditionDisplayContent(fixedEdgesList, fixedAnglesList) {
            let content = '';
            
            // 显示固定的边
            fixedEdgesList.forEach(([edge, _]) => {
                content += `<span class="condition-item edge">边${edge}</span>`;
            });
            
            // 显示固定的角
            fixedAnglesList.forEach(([angle, _]) => {
                content += `<span class="condition-item angle">角${angle}</span>`;
            });
            
            // 显示几何关系类型
            const relationshipDescriptions = {
                'SSS': '三边确定',
                'SAS': '边角边 (两边夹角)',
                'SSA': '边边角 (两边非夹角)',
                'ASA': '角边角 (两角夹边)',
                'AAS': '角角边 (两角对边)',
                'HL': '斜边直角边',
                'S': '单边条件',
                'A': '单角条件',
                'SS': '两边条件',
                'AA': '两角条件',
                'AAA': '三角条件',
                'SA': '边角条件 (边和对应角)',
                'AS': '角边条件 (角和非对应边)'
            };
            
            const relationshipText = `${currentConditionString} - ${relationshipDescriptions[currentConditionString] || '未知'}`;
            content += `<span class="condition-item" style="background: rgba(79, 172, 254, 0.3); color: #4facfe; font-weight: bold;">${relationshipText}</span>`;
            
            return content;
        }
        
        // 获取总固定数量
        function getTotalFixedCount() {
            const fixedEdgesCount = Object.values(fixedEdges).filter(Boolean).length;
            const fixedAnglesCount = Object.values(fixedAngles).filter(Boolean).length;
            return fixedEdgesCount + fixedAnglesCount;
        }
        
        // 检查是否有两个角被固定（用于特殊缩放逻辑）
        function hasTwoFixedAngles() {
            const fixedAnglesCount = Object.values(fixedAngles).filter(Boolean).length;
            return fixedAnglesCount === 2;
        }
        
        // 获取未固定的角（用于特殊缩放逻辑）
        function getUnfixedAngle() {
            for (const [vertex, isFixed] of Object.entries(fixedAngles)) {
                if (!isFixed) {
                    return vertex;
                }
            }
            return null;
        }
        
        // 检查两个固定角之间的边是否也被固定
        function isTwoAnglesEdgeFixed() {
            if (!hasTwoFixedAngles()) {
                return false;
            }
            
            // 获取两个固定的角
            const fixedAngleVertices = Object.entries(fixedAngles)
                .filter(([vertex, isFixed]) => isFixed)
                .map(([vertex]) => vertex);
            
            if (fixedAngleVertices.length !== 2) {
                return false;
            }
            
            // 检查这两个角之间的边是否被固定
            const vertex1 = fixedAngleVertices[0];
            const vertex2 = fixedAngleVertices[1];
            
            // 找到连接这两个顶点的边
            let edgeBetween = null;
            if ((vertex1 === 'A' && vertex2 === 'B') || (vertex1 === 'B' && vertex2 === 'A')) {
                edgeBetween = 'c'; // AB边
            } else if ((vertex1 === 'A' && vertex2 === 'C') || (vertex1 === 'C' && vertex2 === 'A')) {
                edgeBetween = 'b'; // AC边
            } else if ((vertex1 === 'B' && vertex2 === 'C') || (vertex1 === 'C' && vertex2 === 'B')) {
                edgeBetween = 'a'; // BC边
            }
            
            return edgeBetween && fixedEdges[edgeBetween];
        }
        
        // 检查是否可以进行两角固定的等比缩放（排除ASA和AAS情况）
        function canPerformTwoAngleScaling() {
            return hasTwoFixedAngles() && !isTwoAnglesEdgeFixed() && !isAASCondition();
        }
        
        // 检查是否为AAS条件（两角一对边）
        function isAASCondition() {
            const conditionType = analyzeConditionType();
            return conditionType === 'AAS';
        }
        
        // 检查是否为AAA情况（三个角都固定）
        function hasThreeFixedAngles() {
            const fixedAnglesCount = Object.values(fixedAngles).filter(Boolean).length;
            return fixedAnglesCount === 3;
        }
        
        // 检查是否可以进行AAA等比缩放
        function canPerformAAAScaling() {
            return hasThreeFixedAngles();
        }
        
        // 应用精确的几何约束
        function applyGeometricConstraints(draggedVertex, newPos) {
            console.log(`应用几何约束: 拖拽顶点 ${draggedVertex}, 目标位置 (${newPos.x.toFixed(1)}, ${newPos.y.toFixed(1)})`);
            
            // 收集所有相关的约束
            const constraints = collectConstraints(draggedVertex);
            
            if (constraints.length === 0) {
                // 没有约束，直接返回新位置
                console.log('无约束，直接移动');
                return newPos;
            }
            
            // 应用约束并找到最佳位置
            const constrainedPos = findConstrainedPosition(draggedVertex, newPos, constraints);
            
            if (constrainedPos) {
                console.log(`约束后位置: (${constrainedPos.x.toFixed(1)}, ${constrainedPos.y.toFixed(1)})`);
                return constrainedPos;
            } else {
                console.log('无法找到满足约束的位置');
                return null;
            }
        }
        
        // 收集拖拽顶点相关的所有约束
        function collectConstraints(draggedVertex) {
            const constraints = [];
            
            // 检查边长约束
            for (const [edge, isFixed] of Object.entries(fixedEdges)) {
                if (!isFixed) continue;
                
                const vertices = getEdgeVertices(edge);
                if (vertices.includes(draggedVertex)) {
                    // 这条边包含被拖拽的顶点
                    const otherVertex = vertices.find(v => v !== draggedVertex);
                    const fixedLength = initialEdgeLengths[edge];
                    
                    constraints.push({
                        type: 'edge',
                        edge: edge,
                        anchorVertex: otherVertex,
                        draggedVertex: draggedVertex,
                        fixedLength: fixedLength
                    });
                    
                    console.log(`添加边长约束: ${edge} (${draggedVertex} 绕 ${otherVertex} 圆周运动, 距离 ${fixedLength.toFixed(1)})`);
                }
            }
            
            // 检查角度约束
            for (const [vertex, isFixed] of Object.entries(fixedAngles)) {
                if (!isFixed) continue;
                
                const otherVertices = getOtherVertices(vertex);
                if (otherVertices.includes(draggedVertex)) {
                    // 这个角包含被拖拽的顶点
                    const fixedAngle = initialAngles[vertex];
                    
                    constraints.push({
                        type: 'angle',
                        angleVertex: vertex,
                        draggedVertex: draggedVertex,
                        fixedAngle: fixedAngle,
                        otherVertices: otherVertices
                    });
                    
                    console.log(`添加角度约束: 角${vertex} (${draggedVertex} 在角${vertex}的射线上运动, 角度 ${fixedAngle.toFixed(1)}°)`);
                }
            }
            
            return constraints;
        }
        
        // 根据约束找到合适的位置
        function findConstrainedPosition(draggedVertex, targetPos, constraints) {
            if (constraints.length === 0) {
                return targetPos;
            }
            
            if (constraints.length === 1) {
                // 单一约束
                return applySingleConstraint(draggedVertex, targetPos, constraints[0]);
            } else {
                // 多重约束，需要找到交集
                return applyMultipleConstraints(draggedVertex, targetPos, constraints);
            }
        }
        
        // 应用单一约束
        function applySingleConstraint(draggedVertex, targetPos, constraint) {
            if (constraint.type === 'edge') {
                // 边长约束：绕锚点做圆周运动
                return constrainToCircle(
                    triangle[constraint.anchorVertex], 
                    targetPos, 
                    constraint.fixedLength
                );
            } else if (constraint.type === 'angle') {
                // 角度约束：在射线上运动
                return constrainToAngleRay(
                    constraint.angleVertex,
                    constraint.draggedVertex,
                    targetPos,
                    constraint.fixedAngle,
                    constraint.otherVertices
                );
            }
            return targetPos;
        }
        
        // 应用多重约束
        function applyMultipleConstraints(draggedVertex, targetPos, constraints) {
            // 对于多重约束，我们需要找到所有约束的交集
            // 这里使用迭代方法逐步满足每个约束
            
            let currentPos = { ...targetPos };
            const maxIterations = 10;
            
            for (let i = 0; i < maxIterations; i++) {
                let positionChanged = false;
                
                for (const constraint of constraints) {
                    const newPos = applySingleConstraint(draggedVertex, currentPos, constraint);
                    if (newPos && (Math.abs(newPos.x - currentPos.x) > 0.1 || Math.abs(newPos.y - currentPos.y) > 0.1)) {
                        currentPos = newPos;
                        positionChanged = true;
                    }
                }
                
                // 如果位置不再变化，说明收敛了
                if (!positionChanged) {
                    break;
                }
            }
            
            // 验证最终位置是否满足所有约束
            const isValid = constraints.every(constraint => {
                return validateConstraint(draggedVertex, currentPos, constraint);
            });
            
            if (isValid) {
                console.log(`多重约束收敛成功，迭代次数: ${Math.min(maxIterations, constraints.length)}`);
                return currentPos;
            } else {
                console.log('多重约束无法收敛');
                return null;
            }
        }
        
        // 约束到圆周（边长固定）
        function constrainToCircle(center, targetPos, radius) {
            const dx = targetPos.x - center.x;
            const dy = targetPos.y - center.y;
            const distance = Math.sqrt(dx * dx + dy * dy);
            
            if (distance < 0.1) {
                // 避免除零，返回一个默认位置
                return { x: center.x + radius, y: center.y };
            }
            
            // 将目标点投影到圆周上
            const scale = radius / distance;
            return {
                x: center.x + dx * scale,
                y: center.y + dy * scale
            };
        }
        
        // 约束到角度射线（角度固定）
        function constrainToAngleRay(angleVertex, draggedVertex, targetPos, fixedAngle, otherVertices) {
            const angleVertexPos = triangle[angleVertex];
            const otherVertex = otherVertices.find(v => v !== draggedVertex);
            const otherVertexPos = triangle[otherVertex];
            
            // 计算固定边的方向向量
            const fixedEdgeDir = {
                x: otherVertexPos.x - angleVertexPos.x,
                y: otherVertexPos.y - angleVertexPos.y
            };
            
            const fixedEdgeLength = Math.sqrt(fixedEdgeDir.x * fixedEdgeDir.x + fixedEdgeDir.y * fixedEdgeDir.y);
            if (fixedEdgeLength < 0.1) return targetPos;
            
            // 归一化固定边方向
            const fixedEdgeUnit = {
                x: fixedEdgeDir.x / fixedEdgeLength,
                y: fixedEdgeDir.y / fixedEdgeLength
            };
            
            // 计算目标边的期望长度（保持当前长度或使用目标位置的距离）
            const targetDistance = Math.sqrt(
                Math.pow(targetPos.x - angleVertexPos.x, 2) + 
                Math.pow(targetPos.y - angleVertexPos.y, 2)
            );
            
            // 根据固定角度计算新的方向
            const angleRad = fixedAngle * Math.PI / 180;
            
            // 计算两个可能的方向（顺时针和逆时针）
            const cos = Math.cos(angleRad);
            const sin = Math.sin(angleRad);
            
            const dir1 = {
                x: fixedEdgeUnit.x * cos - fixedEdgeUnit.y * sin,
                y: fixedEdgeUnit.x * sin + fixedEdgeUnit.y * cos
            };
            
            const dir2 = {
                x: fixedEdgeUnit.x * cos + fixedEdgeUnit.y * sin,
                y: -fixedEdgeUnit.x * sin + fixedEdgeUnit.y * cos
            };
            
            // 计算两个可能的位置
            const pos1 = {
                x: angleVertexPos.x + dir1.x * targetDistance,
                y: angleVertexPos.y + dir1.y * targetDistance
            };
            
            const pos2 = {
                x: angleVertexPos.x + dir2.x * targetDistance,
                y: angleVertexPos.y + dir2.y * targetDistance
            };
            
            // 选择离目标位置更近的那个
            const dist1 = Math.sqrt(Math.pow(pos1.x - targetPos.x, 2) + Math.pow(pos1.y - targetPos.y, 2));
            const dist2 = Math.sqrt(Math.pow(pos2.x - targetPos.x, 2) + Math.pow(pos2.y - targetPos.y, 2));
            
            return dist1 <= dist2 ? pos1 : pos2;
        }
        
        // 验证约束是否满足
        function validateConstraint(draggedVertex, position, constraint) {
            const tolerance = 1.0; // 容忍度
            
            if (constraint.type === 'edge') {
                const anchorPos = triangle[constraint.anchorVertex];
                const actualDistance = Math.sqrt(
                    Math.pow(position.x - anchorPos.x, 2) + 
                    Math.pow(position.y - anchorPos.y, 2)
                );
                return Math.abs(actualDistance - constraint.fixedLength) < tolerance;
            } else if (constraint.type === 'angle') {
                // 创建临时三角形来验证角度
                const tempTriangle = { ...triangle };
                tempTriangle[draggedVertex] = position;
                
                const actualAngle = calculateAngle(
                    tempTriangle[constraint.angleVertex],
                    tempTriangle[constraint.otherVertices[0]],
                    tempTriangle[constraint.otherVertices[1]]
                );
                
                return Math.abs(actualAngle - constraint.fixedAngle) < tolerance;
            }
            
            return true;
        }
        
        // 等比缩放三角形（保持两个固定角度不变）
        function scaleTriangleProportionally(draggedVertex, newPos) {
            // 计算三角形的重心
            const centroid = {
                x: (triangle.A.x + triangle.B.x + triangle.C.x) / 3,
                y: (triangle.A.y + triangle.B.y + triangle.C.y) / 3
            };
            
            // 计算拖拽顶点到重心的原始距离
            const originalDistance = Math.sqrt(
                Math.pow(triangle[draggedVertex].x - centroid.x, 2) + 
                Math.pow(triangle[draggedVertex].y - centroid.y, 2)
            );
            
            // 计算新位置到重心的距离
            const newDistance = Math.sqrt(
                Math.pow(newPos.x - centroid.x, 2) + 
                Math.pow(newPos.y - centroid.y, 2)
            );
            
            // 如果原始距离太小，避免除零错误
            if (originalDistance < 1) {
                return;
            }
            
            // 计算缩放比例
            const scaleRatio = newDistance / originalDistance;
            
            // 限制缩放比例，避免三角形过大或过小
            const limitedScaleRatio = Math.max(0.1, Math.min(10, scaleRatio));
            
            // 备份当前三角形状态，用于验证角度是否保持
            const backup = {
                A: { ...triangle.A },
                B: { ...triangle.B },
                C: { ...triangle.C }
            };
            
            // 以重心为中心等比缩放所有顶点
            triangle.A.x = centroid.x + (triangle.A.x - centroid.x) * limitedScaleRatio;
            triangle.A.y = centroid.y + (triangle.A.y - centroid.y) * limitedScaleRatio;
            triangle.B.x = centroid.x + (triangle.B.x - centroid.x) * limitedScaleRatio;
            triangle.B.y = centroid.y + (triangle.B.y - centroid.y) * limitedScaleRatio;
            triangle.C.x = centroid.x + (triangle.C.x - centroid.x) * limitedScaleRatio;
            triangle.C.y = centroid.y + (triangle.C.y - centroid.y) * limitedScaleRatio;
            
            // 验证固定角度是否保持（调试用）
            const fixedVertices = Object.entries(fixedAngles).filter(([_, isFixed]) => isFixed).map(([vertex, _]) => vertex);
            if (fixedVertices.length === 2) {
                fixedVertices.forEach(vertex => {
                    const originalAngle = calculateAngle(
                        backup[vertex], 
                        backup[getOtherVertices(vertex)[0]], 
                        backup[getOtherVertices(vertex)[1]]
                    );
                    const newAngle = calculateAngle(
                        triangle[vertex], 
                        triangle[getOtherVertices(vertex)[0]], 
                        triangle[getOtherVertices(vertex)[1]]
                    );
                    const angleDiff = Math.abs(originalAngle - newAngle);
                    if (angleDiff > 0.1) {
                        console.warn(`角度 ${vertex} 发生变化: ${originalAngle.toFixed(1)}° → ${newAngle.toFixed(1)}° (差值: ${angleDiff.toFixed(1)}°)`);
                    }
                });
            }
            
            console.log(`等比缩放三角形: 缩放比例 ${limitedScaleRatio.toFixed(2)}, 拖拽顶点 ${draggedVertex}, 重心 (${centroid.x.toFixed(1)}, ${centroid.y.toFixed(1)})`);
        }
        
        // 显示最大限制提示
        function showMaxLimitMessage() {
            const conditionDisplay = document.getElementById('condition-display');
            const originalContent = conditionDisplay.innerHTML;
            
            conditionDisplay.innerHTML = '<span style="color: #ff9900; font-weight: bold;">⚠️ 最多只能固定3个条件！</span>';
            
            setTimeout(() => {
                conditionDisplay.innerHTML = originalContent;
            }, 2000);
        }
        
        // 显示重复提示
        function showDuplicateMessage() {
            const button = document.getElementById('judge-button');
            const originalText = button.textContent;
            
            button.textContent = '⚠️ 该条件已经测试过了！';
            button.style.background = 'linear-gradient(to right, #ff9900, #ff6600)';
            
            setTimeout(() => {
                button.textContent = originalText;
                button.style.background = 'linear-gradient(to right, #4facfe, #00f2fe)';
            }, 2000);
        }
        
        // 显示判定结果
        function showJudgeResult(isSuccess) {
            const button = document.getElementById('judge-button');
            
            if (isSuccess) {
                button.textContent = '🎉 判定成功！该条件能确定三角形';
                button.style.background = 'linear-gradient(to right, #a0e63c, #4facfe)';
                
                // 触发成功动画
                triggerSuccessAnimation();
            } else {
                button.textContent = '❌ 判定失败！该条件无法唯一确定三角形';
                button.style.background = 'linear-gradient(to right, #ff4b2b, #ff416c)';
                
                // 触发失败动画
                triggerFailureAnimation();
            }
            
            setTimeout(() => {
                // 检查currentConditionString是否有效，避免显示null
                if (currentConditionString && currentConditionString !== 'null') {
                    button.textContent = `🔍 判定 "${currentConditionString}" 是否能确定唯一三角形`;
                } else {
                    button.textContent = '🔍 请先固定至少一个条件';
                    button.disabled = true;
                }
                button.style.background = 'linear-gradient(to right, #4facfe, #00f2fe)';
            }, 3000);
            
            // 调试信息
            console.log(`判定结果: ${currentConditionString} -> ${isSuccess ? '成功' : '失败'}`);
        }
        
        // 更新历史记录显示
        function updateHistoryDisplay() {
            // 构建成功列表HTML
            let successHtml;
            if (successfulConditions.size > 0) {
                successHtml = '<div class="list-title success">✅ 成功条件</div>';
                successfulConditions.forEach(condition => {
                    const conditionName = getConditionDisplayName(condition);
                    successHtml += `<div class="history-item success">
                        <span class="history-condition">${conditionName}</span>
                        <span>能确定三角形</span>
                    </div>`;
                });
            } else {
                successHtml = '<div class="list-title success">✅ 成功条件</div><div class="empty-hint">还没有发现成功的条件</div>';
            }
            
            // 构建失败列表HTML
            let failureHtml;
            if (failedConditions.size > 0) {
                failureHtml = '<div class="list-title failure">❌ 失败条件</div>';
                failedConditions.forEach(condition => {
                    const conditionName = getConditionDisplayName(condition);
                    failureHtml += `<div class="history-item failure">
                        <span class="history-condition">${conditionName}</span>
                        <span>无法确定三角形</span>
                    </div>`;
                });
            } else {
                failureHtml = '<div class="list-title failure">❌ 失败条件</div><div class="empty-hint">还没有尝试失败的条件</div>';
            }
            
            // 更新桌面版
            const successList = document.getElementById('success-list');
            const failureList = document.getElementById('failure-list');
            if (successList) successList.innerHTML = successHtml;
            if (failureList) failureList.innerHTML = failureHtml;
            
            // 更新移动端
            const mobileSuccessList = document.getElementById('mobile-success-list');
            const mobileFailureList = document.getElementById('mobile-failure-list');
            if (mobileSuccessList) mobileSuccessList.innerHTML = successHtml;
            if (mobileFailureList) mobileFailureList.innerHTML = failureHtml;
                         
            // 延迟调整面板位置，确保DOM更新完成
            setTimeout(() => {
                adjustPanelPositions();
            }, 10);
        }
         
         // 触发成功动画
         function triggerSuccessAnimation() {
             // 三角形成功填充动画已在drawTriangle中实现
             // 这里可以添加额外的成功效果
             document.body.style.animation = 'successFlash 1s ease-in-out';
             
             setTimeout(() => {
                 document.body.style.animation = '';
             }, 1000);
         }
         
         // 触发失败动画
         function triggerFailureAnimation() {
             // 添加失败晃动效果
             const canvas = document.getElementById('triangleCanvas');
             canvas.style.animation = 'failureShake 0.5s ease-in-out';
             
             setTimeout(() => {
                 canvas.style.animation = '';
             }, 500);
         }
         
         // 更新绘制逻辑以支持探索模式
         function drawTriangle() {
             // 绘制边
             drawEdge(triangle.B, triangle.C, 'a'); // 边a (BC)
             drawEdge(triangle.A, triangle.C, 'b'); // 边b (AC)
             drawEdge(triangle.A, triangle.B, 'c'); // 边c (AB)
             
             // 根据当前判定结果绘制特殊效果
             if (currentJudgeResult && judgeResultCondition === currentConditionString) {
                 if (currentJudgeResult === 'success') {
                     drawTriangleFill();
                 } else if (currentJudgeResult === 'failure') {
                     drawTriangleFailure();
                 }
             }
             
             // 特殊效果：如果有两个或三个角被固定，绘制提示
             if (hasThreeFixedAngles() || hasTwoFixedAngles()) {
                 drawScalingHint();
             }
             
             // 绘制约束提示（圆周运动、射线运动等）
             drawConstraintHints();
             
                         // 绘制内角角度标注
            drawAngleLabels();
            
            // 绘制顶点
            drawVertex(triangle.A, 'A', '#ffcc00'); // 顶点A - 金黄色
            drawVertex(triangle.B, 'B', '#00f2fe'); // 顶点B - 青蓝色
            drawVertex(triangle.C, 'C', '#a0e63c'); // 顶点C - 绿色
            
            // 绘制橡皮擦预览（仅在橡皮擦模式下且鼠标在画布上时）
            if (eraserMode && drawingMode && mousePos) {
                drawEraserPreview(mousePos.x, mousePos.y);
            }
         }
         
         // 绘制全等完成时的填充效果
         function drawTriangleFill() {
             ctx.beginPath();
             ctx.moveTo(triangle.A.x, triangle.A.y);
             ctx.lineTo(triangle.B.x, triangle.B.y);
             ctx.lineTo(triangle.C.x, triangle.C.y);
             ctx.closePath();
             
             // 成功的半透明绿色填充
             ctx.fillStyle = 'rgba(160, 230, 60, 0.15)';
             ctx.fill();
             
             // 添加发光效果
             ctx.strokeStyle = 'rgba(160, 230, 60, 0.8)';
             ctx.lineWidth = 3 / transform.scale;
             ctx.setLineDash([]);
             ctx.stroke();
         }
         
         // 绘制判定失败效果
         function drawTriangleFailure() {
             ctx.beginPath();
             ctx.moveTo(triangle.A.x, triangle.A.y);
             ctx.lineTo(triangle.B.x, triangle.B.y);
             ctx.lineTo(triangle.C.x, triangle.C.y);
             ctx.closePath();
             
             // 失败的半透明红色填充
             ctx.fillStyle = 'rgba(255, 75, 43, 0.1)';
             ctx.fill();
             
             // 添加红色虚线边框
             ctx.strokeStyle = 'rgba(255, 75, 43, 0.8)';
             ctx.lineWidth = 3 / transform.scale;
             ctx.setLineDash([10 / transform.scale, 5 / transform.scale]);
             ctx.stroke();
         }
         
         // 绘制缩放提示效果（两角固定时）
         function drawScalingHint() {
             // 计算三角形重心
             const centroid = {
                 x: (triangle.A.x + triangle.B.x + triangle.C.x) / 3,
                 y: (triangle.A.y + triangle.B.y + triangle.C.y) / 3
             };
             
             // 绘制重心点
             ctx.save();
             ctx.beginPath();
             ctx.arc(centroid.x, centroid.y, 4 / transform.scale, 0, Math.PI * 2);
             ctx.fillStyle = 'rgba(255, 204, 0, 0.8)';
             ctx.fill();
             ctx.strokeStyle = 'rgba(255, 204, 0, 1)';
             ctx.lineWidth = 2 / transform.scale;
             ctx.stroke();
             ctx.restore();
             
             // 绘制从重心到各顶点的虚线（在可缩放情况下）
             if (canPerformAAAScaling() || canPerformTwoAngleScaling()) {
                 ctx.save();
                 ctx.strokeStyle = 'rgba(255, 204, 0, 0.5)';
                 ctx.lineWidth = 1 / transform.scale;
                 ctx.setLineDash([5 / transform.scale, 5 / transform.scale]);
                 
                 // 到顶点A的线
                 ctx.beginPath();
                 ctx.moveTo(centroid.x, centroid.y);
                 ctx.lineTo(triangle.A.x, triangle.A.y);
                 ctx.stroke();
                 
                 // 到顶点B的线
                 ctx.beginPath();
                 ctx.moveTo(centroid.x, centroid.y);
                 ctx.lineTo(triangle.B.x, triangle.B.y);
                 ctx.stroke();
                 
                 // 到顶点C的线
                 ctx.beginPath();
                 ctx.moveTo(centroid.x, centroid.y);
                 ctx.lineTo(triangle.C.x, triangle.C.y);
                 ctx.stroke();
                 
                 ctx.restore();
             }
             
             // 高亮显示可拖拽进行缩放的顶点
             if (canPerformAAAScaling()) {
                 // AAA情况：高亮所有三个顶点
                 ['A', 'B', 'C'].forEach(vertex => {
                     if (triangle[vertex]) {
                         ctx.save();
                         ctx.beginPath();
                         ctx.arc(triangle[vertex].x, triangle[vertex].y, 18 / transform.scale, 0, Math.PI * 2);
                         ctx.strokeStyle = 'rgba(255, 204, 0, 0.8)';
                         ctx.lineWidth = 3 / transform.scale;
                         ctx.setLineDash([8 / transform.scale, 4 / transform.scale]);
                         ctx.stroke();
                         ctx.restore();
                     }
                 });
             } else {
                 // 两角固定的情况
                 const unfixedVertex = getUnfixedAngle();
                 if (unfixedVertex && triangle[unfixedVertex] && canPerformTwoAngleScaling()) {
                     ctx.save();
                     ctx.beginPath();
                     ctx.arc(triangle[unfixedVertex].x, triangle[unfixedVertex].y, 18 / transform.scale, 0, Math.PI * 2);
                     ctx.strokeStyle = 'rgba(255, 204, 0, 0.8)';
                     ctx.lineWidth = 3 / transform.scale;
                     ctx.setLineDash([8 / transform.scale, 4 / transform.scale]);
                     ctx.stroke();
                     ctx.restore();
                 } else if (unfixedVertex && triangle[unfixedVertex] && (isTwoAnglesEdgeFixed() || isAASCondition())) {
                     // ASA或AAS情况：显示红色禁止标识
                     ctx.save();
                     ctx.beginPath();
                     ctx.arc(triangle[unfixedVertex].x, triangle[unfixedVertex].y, 18 / transform.scale, 0, Math.PI * 2);
                     ctx.strokeStyle = 'rgba(255, 75, 43, 0.8)';
                     ctx.lineWidth = 3 / transform.scale;
                     ctx.setLineDash([]);
                     ctx.stroke();
                     
                     // 绘制禁止符号（斜线）
                     ctx.beginPath();
                     ctx.moveTo(
                         triangle[unfixedVertex].x - 12 / transform.scale, 
                         triangle[unfixedVertex].y - 12 / transform.scale
                     );
                     ctx.lineTo(
                         triangle[unfixedVertex].x + 12 / transform.scale, 
                         triangle[unfixedVertex].y + 12 / transform.scale
                     );
                     ctx.stroke();
                     
                     ctx.restore();
                 }
             }
             
             // 绘制提示文字
             ctx.save();
             ctx.font = `bold ${14 / transform.scale}px Arial`;
             ctx.fillStyle = 'rgba(255, 204, 0, 0.9)';
             ctx.strokeStyle = 'rgba(0, 0, 0, 0.8)';
             ctx.lineWidth = 3 / transform.scale;
             ctx.textAlign = 'center';
             ctx.textBaseline = 'middle';
             
             let hintText;
             if (canPerformAAAScaling()) {
                 // AAA情况：可以拖拽任何顶点缩放
                 hintText = `拖拽任何顶点可缩放三角形 (AAA)`;
             } else if (isTwoAnglesEdgeFixed()) {
                 // ASA情况：三角形已完全确定
                 hintText = `三角形已完全确定 (ASA)`;
             } else if (isAASCondition()) {
                 // AAS情况：三角形已完全确定
                 hintText = `三角形已完全确定 (AAS)`;
             } else {
                 // AA情况：可以缩放
                 const unfixedVertex = getUnfixedAngle();
                 hintText = `拖拽 ${unfixedVertex} 顶点可缩放三角形`;
             }
             const hintY = centroid.y - 40 / transform.scale;
             
             // 绘制文字描边
             ctx.strokeText(hintText, centroid.x, hintY);
             // 绘制文字填充
             ctx.fillText(hintText, centroid.x, hintY);
             
             ctx.restore();
         }
         
         // 绘制角度标注
         function drawAngleLabels() {
             if (!triangle) return;
             
             // 计算三个角度
             const angleA = calculateAngle(triangle.A, triangle.B, triangle.C);
             const angleB = calculateAngle(triangle.B, triangle.A, triangle.C);
             const angleC = calculateAngle(triangle.C, triangle.A, triangle.B);
             
             // 绘制角A的标注
             drawAngleLabel(triangle.A, triangle.B, triangle.C, angleA, 'A');
             
             // 绘制角B的标注
             drawAngleLabel(triangle.B, triangle.A, triangle.C, angleB, 'B');
             
             // 绘制角C的标注
             drawAngleLabel(triangle.C, triangle.A, triangle.B, angleC, 'C');
         }
         
         // 绘制单个角度标注
         function drawAngleLabel(vertex, point1, point2, angle, label) {
             // 计算从顶点到两个点的向量
             const vec1 = {
                 x: point1.x - vertex.x,
                 y: point1.y - vertex.y
             };
             const vec2 = {
                 x: point2.x - vertex.x,
                 y: point2.y - vertex.y
             };
             
             // 归一化向量
             const len1 = Math.sqrt(vec1.x * vec1.x + vec1.y * vec1.y);
             const len2 = Math.sqrt(vec2.x * vec2.x + vec2.y * vec2.y);
             
             if (len1 < 0.1 || len2 < 0.1) return;
             
             const unit1 = { x: vec1.x / len1, y: vec1.y / len1 };
             const unit2 = { x: vec2.x / len2, y: vec2.y / len2 };
             
             // 计算角度的平分线方向
             const bisector = {
                 x: (unit1.x + unit2.x) / 2,
                 y: (unit1.y + unit2.y) / 2
             };
             
             // 归一化平分线向量
             const bisectorLen = Math.sqrt(bisector.x * bisector.x + bisector.y * bisector.y);
             if (bisectorLen < 0.1) return;
             
             const unitBisector = {
                 x: bisector.x / bisectorLen,
                 y: bisector.y / bisectorLen
             };
             
             // 计算标注位置（沿角平分线向内偏移）
             const offset = 30 / transform.scale; // 标注距离顶点的距离
             const labelPos = {
                 x: vertex.x + unitBisector.x * offset,
                 y: vertex.y + unitBisector.y * offset
             };
             
             // 绘制角度弧线
             drawAngleArc(vertex, unit1, unit2, 20 / transform.scale, label);
             
             // 绘制角度文本
             ctx.save();
             ctx.font = `bold ${12 / transform.scale}px Arial`;
             ctx.fillStyle = fixedAngles[label] ? '#ff4b2b' : '#fff';
             ctx.textAlign = 'center';
             ctx.textBaseline = 'middle';
             ctx.strokeStyle = 'rgba(0, 0, 0, 0.8)';
             ctx.lineWidth = 3 / transform.scale;
             
             const angleText = angle.toFixed(0) + '°';
             
             // 绘制文字描边
             ctx.strokeText(angleText, labelPos.x, labelPos.y);
             // 绘制文字填充
             ctx.fillText(angleText, labelPos.x, labelPos.y);
             
             ctx.restore();
         }
         
         // 绘制角度弧线
         function drawAngleArc(vertex, unit1, unit2, radius, label) {
             // 计算起始和结束角度
             const startAngle = Math.atan2(unit1.y, unit1.x);
             const endAngle = Math.atan2(unit2.y, unit2.x);
             
             // 确保弧线方向正确（取较小的角度）
             let sweepAngle = endAngle - startAngle;
             if (sweepAngle > Math.PI) sweepAngle -= 2 * Math.PI;
             if (sweepAngle < -Math.PI) sweepAngle += 2 * Math.PI;
             
             // 绘制弧线
             ctx.save();
             ctx.beginPath();
             ctx.arc(vertex.x, vertex.y, radius, startAngle, startAngle + sweepAngle, sweepAngle < 0);
             
             // 设置弧线样式
             ctx.strokeStyle = fixedAngles[label] ? '#ff4b2b' : 'rgba(255, 255, 255, 0.6)';
             ctx.lineWidth = 2 / transform.scale;
             ctx.setLineDash([]);
             ctx.stroke();
             
             ctx.restore();
         }
         
         // 绘制约束提示
         function drawConstraintHints() {
             let constraintsToShow = null;
             let vertexToShow = null;
             
             if (drawingMode && persistentConstraints && persistentDraggedVertex) {
                 // 画笔模式：显示持久化的约束
                 constraintsToShow = persistentConstraints;
                 vertexToShow = persistentDraggedVertex;
             } else if (isVertexDragging && draggedVertex && !drawingMode) {
                 // 正常拖拽模式：显示当前约束
                 constraintsToShow = collectConstraints(draggedVertex);
                 vertexToShow = draggedVertex;
                 
                 // 更新持久化约束（为后续画笔模式准备）
                 persistentConstraints = constraintsToShow;
                 persistentDraggedVertex = vertexToShow;
             }
             
             // 绘制约束
             if (constraintsToShow && constraintsToShow.length > 0) {
                 constraintsToShow.forEach(constraint => {
                     if (constraint.type === 'edge') {
                         // 绘制圆周路径（边长约束）
                         drawCircularConstraint(constraint);
                     } else if (constraint.type === 'angle') {
                         // 绘制射线路径（角度约束）
                         drawAngularConstraint(constraint);
                     }
                 });
             }
         }
         
         // 绘制圆周约束（边长固定）
         function drawCircularConstraint(constraint) {
             const center = triangle[constraint.anchorVertex];
             const radius = constraint.fixedLength;
             
             ctx.save();
             ctx.beginPath();
             ctx.arc(center.x, center.y, radius, 0, Math.PI * 2);
             ctx.strokeStyle = 'rgba(255, 165, 0, 0.6)'; // 橙色
             ctx.lineWidth = 2 / transform.scale;
             ctx.setLineDash([8 / transform.scale, 4 / transform.scale]);
             ctx.stroke();
             
             // 绘制中心点
             ctx.beginPath();
             ctx.arc(center.x, center.y, 3 / transform.scale, 0, Math.PI * 2);
             ctx.fillStyle = 'rgba(255, 165, 0, 0.8)';
             ctx.fill();
             
             // 绘制提示文字
             ctx.font = `bold ${12 / transform.scale}px Arial`;
             ctx.fillStyle = 'rgba(255, 165, 0, 0.9)';
             ctx.strokeStyle = 'rgba(0, 0, 0, 0.8)';
             ctx.lineWidth = 2 / transform.scale;
             ctx.textAlign = 'center';
             ctx.textBaseline = 'middle';
             
             const hintText = `${constraint.draggedVertex} 绕 ${constraint.anchorVertex} 圆周运动`;
             const hintY = center.y - radius - 20 / transform.scale;
             
             ctx.strokeText(hintText, center.x, hintY);
             ctx.fillText(hintText, center.x, hintY);
             
             ctx.restore();
         }
         
         // 绘制角度约束（角度固定）
         function drawAngularConstraint(constraint) {
             const angleVertex = triangle[constraint.angleVertex];
             const otherVertex = constraint.otherVertices.find(v => v !== constraint.draggedVertex);
             const otherVertexPos = triangle[otherVertex];
             
             // 计算射线方向
             const fixedEdgeDir = {
                 x: otherVertexPos.x - angleVertex.x,
                 y: otherVertexPos.y - angleVertex.y
             };
             
             const fixedEdgeLength = Math.sqrt(fixedEdgeDir.x * fixedEdgeDir.x + fixedEdgeDir.y * fixedEdgeDir.y);
             if (fixedEdgeLength < 0.1) return;
             
             const fixedEdgeUnit = {
                 x: fixedEdgeDir.x / fixedEdgeLength,
                 y: fixedEdgeDir.y / fixedEdgeLength
             };
             
             // 计算两条射线的方向
             const angleRad = constraint.fixedAngle * Math.PI / 180;
             const cos = Math.cos(angleRad);
             const sin = Math.sin(angleRad);
             
             const ray1Dir = {
                 x: fixedEdgeUnit.x * cos - fixedEdgeUnit.y * sin,
                 y: fixedEdgeUnit.x * sin + fixedEdgeUnit.y * cos
             };
             
             const ray2Dir = {
                 x: fixedEdgeUnit.x * cos + fixedEdgeUnit.y * sin,
                 y: -fixedEdgeUnit.x * sin + fixedEdgeUnit.y * cos
             };
             
             // 绘制两条射线
             const rayLength = 200 / transform.scale;
             
             ctx.save();
             ctx.strokeStyle = 'rgba(138, 43, 226, 0.6)'; // 紫色
             ctx.lineWidth = 2 / transform.scale;
             ctx.setLineDash([12 / transform.scale, 6 / transform.scale]);
             
             // 射线1
             ctx.beginPath();
             ctx.moveTo(angleVertex.x, angleVertex.y);
             ctx.lineTo(
                 angleVertex.x + ray1Dir.x * rayLength,
                 angleVertex.y + ray1Dir.y * rayLength
             );
             ctx.stroke();
             
             // 射线2
             ctx.beginPath();
             ctx.moveTo(angleVertex.x, angleVertex.y);
             ctx.lineTo(
                 angleVertex.x + ray2Dir.x * rayLength,
                 angleVertex.y + ray2Dir.y * rayLength
             );
             ctx.stroke();
             
             // 绘制角度弧线
             const arcRadius = 30 / transform.scale;
             const startAngle = Math.atan2(fixedEdgeUnit.y, fixedEdgeUnit.x);
             const endAngle1 = Math.atan2(ray1Dir.y, ray1Dir.x);
             const endAngle2 = Math.atan2(ray2Dir.y, ray2Dir.x);
             
             ctx.strokeStyle = 'rgba(138, 43, 226, 0.8)';
             ctx.lineWidth = 1 / transform.scale;
             ctx.setLineDash([]);
             
             // 弧线1
             ctx.beginPath();
             ctx.arc(angleVertex.x, angleVertex.y, arcRadius, startAngle, endAngle1, false);
             ctx.stroke();
             
             // 弧线2
             ctx.beginPath();
             ctx.arc(angleVertex.x, angleVertex.y, arcRadius, startAngle, endAngle2, true);
             ctx.stroke();
             
             // 绘制提示文字
             ctx.font = `bold ${12 / transform.scale}px Arial`;
             ctx.fillStyle = 'rgba(138, 43, 226, 0.9)';
             ctx.strokeStyle = 'rgba(0, 0, 0, 0.8)';
             ctx.lineWidth = 2 / transform.scale;
             ctx.textAlign = 'center';
             ctx.textBaseline = 'middle';
             
             const hintText = `${constraint.draggedVertex} 在角${constraint.angleVertex}射线上运动`;
             const hintY = angleVertex.y - 50 / transform.scale;
             
             ctx.strokeText(hintText, angleVertex.x, hintY);
             ctx.fillText(hintText, angleVertex.x, hintY);
             
             ctx.restore();
         }
         
         // 绘制橡皮擦预览
         function drawEraserPreview(x, y) {
             const radius = eraserSize / transform.scale;
             
             ctx.save();
             ctx.beginPath();
             ctx.arc(x, y, radius, 0, Math.PI * 2);
             ctx.strokeStyle = 'rgba(255, 165, 0, 0.8)'; // 橙色边框
             ctx.lineWidth = 2 / transform.scale;
             ctx.setLineDash([5 / transform.scale, 5 / transform.scale]);
             ctx.stroke();
             
             // 绘制半透明填充
             ctx.fillStyle = 'rgba(255, 165, 0, 0.1)';
             ctx.fill();
             
             // 绘制中心点
             ctx.beginPath();
             ctx.arc(x, y, 2 / transform.scale, 0, Math.PI * 2);
             ctx.fillStyle = 'rgba(255, 165, 0, 0.8)';
             ctx.fill();
             
             ctx.restore();
         }
         
         // 橡皮擦功能：在指定位置擦除画笔痕迹
         function eraseAtPosition(x, y) {
             const eraseRadius = eraserSize / transform.scale;
             let hasErased = false;
             
             // 遍历所有路径，检查是否与橡皮擦区域相交
             for (let i = drawingPaths.length - 1; i >= 0; i--) {
                 const path = drawingPaths[i];
                 const newPoints = [];
                 let currentSegment = [];
                 
                 // 检查路径中的每个点
                 for (let j = 0; j < path.points.length; j++) {
                     const point = path.points[j];
                     const distance = Math.sqrt((point.x - x) ** 2 + (point.y - y) ** 2);
                     
                     if (distance > eraseRadius) {
                         // 点在橡皮擦范围外，保留
                         currentSegment.push(point);
                     } else {
                         // 点在橡皮擦范围内，需要擦除
                         hasErased = true;
                         
                         // 如果当前段有点，保存为新路径
                         if (currentSegment.length > 1) {
                             const newPath = {
                                 points: [...currentSegment],
                                 color: path.color,
                                 size: path.size
                             };
                             newPoints.push(newPath);
                         }
                         currentSegment = [];
                     }
                 }
                 
                 // 处理最后一段
                 if (currentSegment.length > 1) {
                     const newPath = {
                         points: [...currentSegment],
                         color: path.color,
                         size: path.size
                     };
                     newPoints.push(newPath);
                 }
                 
                 // 如果路径被分割了，替换原路径
                 if (hasErased) {
                     drawingPaths.splice(i, 1, ...newPoints);
                 }
             }
             
             if (hasErased) {
                 drawScene();
             }
         }
         
         // 关闭画笔工具
        function closeDrawingTool() {
            if (drawingMode) {
                drawingMode = false;
                eraserMode = false;
                isDrawing = false;
                isErasing = false;
                currentPath = null;
                
                // 更新UI状态
                const button = document.getElementById('toggle-drawing');
                const controls = document.getElementById('drawing-controls');
                
                button.textContent = '开启画笔';
                button.style.background = '';
                button.style.color = '';
                controls.style.display = 'none';
                canvas.style.cursor = 'grab';
                
                // 隐藏橡皮擦控件
                const eraserControls = document.getElementById('eraser-controls');
                const mobileEraserControls = document.getElementById('mobile-eraser-controls');
                if (eraserControls) eraserControls.style.display = 'none';
                if (mobileEraserControls) mobileEraserControls.style.display = 'none';
            }
        }
        
        // 初始化画笔工具
        function initDrawingTool() {
            // 切换绘画模式函数
            function toggleDrawingMode() {
                drawingMode = !drawingMode;
                
                // 获取所有相关元素
                const toggleBtn = document.getElementById('toggle-drawing');
                const controls = document.getElementById('drawing-controls');
                const mobileToggleBtn = document.getElementById('mobile-toggle-drawing');
                const mobileControls = document.getElementById('mobile-drawing-controls');
                
                if (drawingMode) {
                    // 开启画笔模式
                    const activeText = '关闭画笔';
                    const activeStyle = { background: '#ff6b6b', color: 'white' };
                    
                    if (toggleBtn) {
                        toggleBtn.textContent = activeText;
                        Object.assign(toggleBtn.style, activeStyle);
                    }
                    if (mobileToggleBtn) {
                        mobileToggleBtn.textContent = activeText;
                        Object.assign(mobileToggleBtn.style, activeStyle);
                    }
                    if (controls) controls.style.display = 'block';
                    if (mobileControls) mobileControls.style.display = 'block';
                    canvas.style.cursor = 'crosshair';
                    
                    // 如果当前正在拖拽顶点，保存约束状态以便在画笔模式下继续显示
                    if (isVertexDragging && draggedVertex) {
                        persistentConstraints = collectConstraints(draggedVertex);
                        persistentDraggedVertex = draggedVertex;
                    }
                    
                } else {
                    // 关闭画笔模式
                    const inactiveText = '开启画笔';
                    const inactiveStyle = { background: '', color: '' };
                    
                    if (toggleBtn) {
                        toggleBtn.textContent = inactiveText;
                        Object.assign(toggleBtn.style, inactiveStyle);
                    }
                    if (mobileToggleBtn) {
                        mobileToggleBtn.textContent = inactiveText;
                        Object.assign(mobileToggleBtn.style, inactiveStyle);
                    }
                    if (controls) controls.style.display = 'none';
                    if (mobileControls) mobileControls.style.display = 'none';
                    canvas.style.cursor = 'grab';
                    
                    // 关闭橡皮擦模式
                    eraserMode = false;
                    const eraserControls = document.getElementById('eraser-controls');
                    const mobileEraserControls = document.getElementById('mobile-eraser-controls');
                    if (eraserControls) eraserControls.style.display = 'none';
                    if (mobileEraserControls) mobileEraserControls.style.display = 'none';
                    
                    // 如果正在绘画或擦除，停止操作
                    if (isDrawing) {
                        isDrawing = false;
                        currentPath = null;
                    }
                    if (isErasing) {
                        isErasing = false;
                    }
                    
                    // 关闭画笔模式时，清除持久约束显示（让正常拖拽逻辑接管）
                    // 注意：不立即清除，让用户可以继续看到约束，直到下次拖拽
                }
                
                // 重新绘制以更新约束显示
                drawScene();
            }
            
            // 切换橡皮擦模式函数
            function toggleEraserMode() {
                eraserMode = !eraserMode;
                
                // 获取所有相关元素
                const eraserBtn = document.getElementById('toggle-eraser');
                const mobileEraserBtn = document.getElementById('mobile-toggle-eraser');
                const eraserControls = document.getElementById('eraser-controls');
                const mobileEraserControls = document.getElementById('mobile-eraser-controls');
                
                if (eraserMode) {
                    // 开启橡皮擦模式
                    const activeStyle = { background: '#ffa500', color: 'white' };
                    const activeText = '🧽 关闭橡皮擦';
                    
                    if (eraserBtn) {
                        eraserBtn.textContent = activeText;
                        Object.assign(eraserBtn.style, activeStyle);
                    }
                    if (mobileEraserBtn) {
                        mobileEraserBtn.textContent = activeText;
                        Object.assign(mobileEraserBtn.style, activeStyle);
                    }
                    if (eraserControls) eraserControls.style.display = 'block';
                    if (mobileEraserControls) mobileEraserControls.style.display = 'block';
                    
                    canvas.style.cursor = 'crosshair';
                } else {
                    // 关闭橡皮擦模式
                    const inactiveStyle = { background: '', color: '' };
                    const inactiveText = '🧽 橡皮擦';
                    
                    if (eraserBtn) {
                        eraserBtn.textContent = inactiveText;
                        Object.assign(eraserBtn.style, inactiveStyle);
                    }
                    if (mobileEraserBtn) {
                        mobileEraserBtn.textContent = inactiveText;
                        Object.assign(mobileEraserBtn.style, inactiveStyle);
                    }
                    if (eraserControls) eraserControls.style.display = 'none';
                    if (mobileEraserControls) mobileEraserControls.style.display = 'none';
                    
                    canvas.style.cursor = 'crosshair';
                    
                    // 如果正在擦除，停止擦除
                    if (isErasing) {
                        isErasing = false;
                    }
                }
            }
            
            // 颜色改变函数
            function handleColorChange(value) {
                brushColor = value;
                // 同步到另一个颜色选择器
                const colorInput = document.getElementById('brush-color');
                const mobileColorInput = document.getElementById('mobile-brush-color');
                if (colorInput && colorInput.value !== value) colorInput.value = value;
                if (mobileColorInput && mobileColorInput.value !== value) mobileColorInput.value = value;
            }
            
            // 大小改变函数
            function handleSizeChange(value) {
                brushSize = parseInt(value);
                // 同步到另一个大小滑块
                const sizeInput = document.getElementById('brush-size');
                const mobileSizeInput = document.getElementById('mobile-brush-size');
                if (sizeInput && sizeInput.value !== value) sizeInput.value = value;
                if (mobileSizeInput && mobileSizeInput.value !== value) mobileSizeInput.value = value;
            }
            
            // 橡皮擦大小改变函数
            function handleEraserSizeChange(value) {
                eraserSize = parseInt(value);
                // 同步到另一个橡皮擦大小滑块
                const eraserSizeInput = document.getElementById('eraser-size');
                const mobileEraserSizeInput = document.getElementById('mobile-eraser-size');
                if (eraserSizeInput && eraserSizeInput.value !== value) eraserSizeInput.value = value;
                if (mobileEraserSizeInput && mobileEraserSizeInput.value !== value) mobileEraserSizeInput.value = value;
            }
            
            // 清除画笔函数
            function clearDrawings() {
                drawingPaths = [];
                currentPath = null;
                isDrawing = false;
                drawScene();
            }
            
            // 桌面版事件监听
            const toggleBtn = document.getElementById('toggle-drawing');
            const colorInput = document.getElementById('brush-color');
            const sizeInput = document.getElementById('brush-size');
            const eraserBtn = document.getElementById('toggle-eraser');
            const eraserSizeInput = document.getElementById('eraser-size');
            const clearBtn = document.getElementById('clear-drawings');
            
            if (toggleBtn) toggleBtn.addEventListener('click', toggleDrawingMode);
            if (colorInput) colorInput.addEventListener('change', (e) => handleColorChange(e.target.value));
            if (sizeInput) sizeInput.addEventListener('input', (e) => handleSizeChange(e.target.value));
            if (eraserBtn) eraserBtn.addEventListener('click', toggleEraserMode);
            if (eraserSizeInput) eraserSizeInput.addEventListener('input', (e) => handleEraserSizeChange(e.target.value));
            if (clearBtn) clearBtn.addEventListener('click', clearDrawings);
            
            // 移动端事件监听
            const mobileToggleBtn = document.getElementById('mobile-toggle-drawing');
            const mobileColorInput = document.getElementById('mobile-brush-color');
            const mobileSizeInput = document.getElementById('mobile-brush-size');
            const mobileEraserBtn = document.getElementById('mobile-toggle-eraser');
            const mobileEraserSizeInput = document.getElementById('mobile-eraser-size');
            const mobileClearBtn = document.getElementById('mobile-clear-drawings');
            
            if (mobileToggleBtn) mobileToggleBtn.addEventListener('click', toggleDrawingMode);
            if (mobileColorInput) mobileColorInput.addEventListener('change', (e) => handleColorChange(e.target.value));
            if (mobileSizeInput) mobileSizeInput.addEventListener('input', (e) => handleSizeChange(e.target.value));
            if (mobileEraserBtn) mobileEraserBtn.addEventListener('click', toggleEraserMode);
            if (mobileEraserSizeInput) mobileEraserSizeInput.addEventListener('input', (e) => handleEraserSizeChange(e.target.value));
            if (mobileClearBtn) mobileClearBtn.addEventListener('click', clearDrawings);
        }
        
        // 显示总结模态框
        function showSummaryModal() {
            const modal = document.getElementById('summary-modal');
            modal.style.display = 'flex';
            
            // 更新总结内容
            updateSummaryContent();
            
            // 添加显示动画
            setTimeout(() => {
                modal.classList.add('show');
            }, 10);
        }
        
        // 关闭总结模态框
        function closeSummaryModal() {
            const modal = document.getElementById('summary-modal');
            modal.classList.remove('show');
            
            // 延迟隐藏，等待动画完成
            setTimeout(() => {
                modal.style.display = 'none';
            }, 300);
        }
        
        // 更新总结内容
        function updateSummaryContent() {
            const successSummary = document.getElementById('success-summary');
            const failureSummary = document.getElementById('failure-summary');
            
            // 更新成功条件总结
            if (successfulConditions.size > 0) {
                let successHtml = '';
                successfulConditions.forEach(condition => {
                    const explanation = getConditionExplanation(condition, true);
                    const displayName = getConditionDisplayName(condition);
                    successHtml += `
                        <div class="condition-summary-item success">
                            <div class="condition-title success">
                                <span class="condition-badge">${condition}</span>
                                <span>${displayName}</span>
                            </div>
                            <div class="condition-explanation">${explanation.description}</div>
                        </div>
                    `;
                });
                successSummary.innerHTML = successHtml;
            } else {
                successSummary.innerHTML = '<div class="empty-summary">还没有发现成功的条件，继续探索吧！<br/>💡 试试固定三条边(SSS)或两边夹角(SAS)等条件</div>';
            }
            
            // 更新失败条件总结
            if (failedConditions.size > 0) {
                let failureHtml = '';
                failedConditions.forEach(condition => {
                    const explanation = getConditionExplanation(condition, false);
                    const displayName = getConditionDisplayName(condition);
                    failureHtml += `
                        <div class="condition-summary-item failure">
                            <div class="condition-title failure">
                                <span class="condition-badge">${condition}</span>
                                <span>${displayName}</span>
                            </div>
                            <div class="condition-explanation">${explanation.description}</div>
                        </div>
                    `;
                });
                failureSummary.innerHTML = failureHtml;
            } else {
                failureSummary.innerHTML = '<div class="empty-summary">还没有尝试失败的条件，勇敢尝试吧！<br/>🤔 试试只固定一条边(S)或一个角(A)看看会怎样</div>';
            }
        }
        
        // 获取条件的显示名称
        function getConditionDisplayName(condition) {
            const displayNames = {
                'SSS': 'SSS（三边确定）',
                'SAS': 'SAS（边角边）',
                'SSA': 'SSA（边边角）',
                'ASA': 'ASA（角边角）',
                'AAS': 'AAS（角角边）',
                'HL': 'HL（斜边直角边）',
                'S': 'S（单边条件）',
                'A': 'A（单角条件）',
                'SS': 'SS（两边条件）',
                'AA': 'AA（两角条件）',
                'AAA': 'AAA（三角条件）',
                'SA': 'SA（边角条件）',
                'AS': 'AS（角边条件）'
            };
            
            return displayNames[condition] || condition;
        }
        
        // 获取条件的详细说明（适合孩子理解）
        function getConditionExplanation(condition, isSuccess) {
            const explanations = {
                // 成功的条件说明
                'SSS': {
                    title: '三边确定',
                    success: '当我们知道三角形的三条边长时，这个三角形的形状就完全确定了！就像用三根固定长度的小棒，只能拼成一种三角形。',
                    failure: '这种情况理论上不会失败，如果出现了可能是程序问题哦。'
                },
                'SAS': {
                    title: '边角边（两边夹角）',
                    success: '当我们知道两条边和它们中间夹着的角度时，三角形就确定了！就像张开手臂的角度固定，手臂长度也固定，整个姿势就确定了。',
                    failure: '这种情况理论上不会失败，如果出现了可能是程序问题哦。'
                },
                'ASA': {
                    title: '角边角（两角夹边）',
                    success: '当我们知道两个角度和它们中间夹着的边时，三角形就确定了！就像知道了一条线段和它两端的方向，整个三角形就画出来了。',
                    failure: '这种情况理论上不会失败，如果出现了可能是程序问题哦。'
                },
                'AAS': {
                    title: '角角边（两角对边）',
                    success: '当我们知道两个角度和其中一个角的对边时，三角形也能确定！因为三角形内角和是180°，第三个角就能算出来，然后就变成了ASA的情况。',
                    failure: '这种情况理论上不会失败，如果出现了可能是程序问题哦。'
                },
                'HL': {
                    title: '斜边直角边',
                    success: '在直角三角形中，当我们知道斜边（最长的边）和一条直角边时，三角形就确定了！这是直角三角形的特殊性质。',
                    failure: '这种情况理论上不会失败，如果出现了可能是程序问题哦。'
                },
                'SSA': {
                    title: '边边角（两边非夹角）',
                    success: '这种情况理论上不会成功，如果出现了可能是程序问题哦。',
                    failure: '当我们知道两条边和不是它们夹角的另一个角时，可能画出两个不同的三角形！就像用圆规画圆，可能有两个交点。'
                },
                'S': {
                    title: '单边条件',
                    success: '这种情况理论上不会成功，如果出现了可能是程序问题哦。',
                    failure: '只知道一条边的长度，显然不能确定三角形的形状。就像只知道一根小棒的长度，还需要知道其他信息才能拼成三角形。'
                },
                'A': {
                    title: '单角条件',
                    success: '这种情况理论上不会成功，如果出现了可能是程序问题哦。',
                    failure: '只知道一个角度，不能确定三角形的大小。就像只知道张开手臂的角度，但不知道手臂长度，无法确定具体的姿势。'
                },
                'SS': {
                    title: '两边条件',
                    success: '这种情况理论上不会成功，如果出现了可能是程序问题哦。',
                    failure: '只知道两条边的长度，但不知道它们的夹角，可以画出无数个不同的三角形。就像两根小棒可以组成很多种角度。'
                },
                'AA': {
                    title: '两角条件',
                    success: '这种情况理论上不会成功，如果出现了可能是程序问题哦。',
                    failure: '只知道两个角度，虽然第三个角能算出来，但不知道边长，可以画出无数个相似但大小不同的三角形。'
                },
                'AAA': {
                    title: '三角条件',
                    success: '这种情况理论上不会成功，如果出现了可能是程序问题哦。',
                    failure: '知道三个角度只能确定三角形的形状，但不能确定大小。就像知道一个三角形是"锐角三角形"，但不知道具体有多大，可以画出无数个相似的三角形。'
                },
                'SA': {
                    title: '边角条件（边和对应角）',
                    success: '这种情况理论上不会成功，如果出现了可能是程序问题哦。',
                    failure: '知道一条边和一个角，但信息还不够确定三角形的形状。需要更多的约束条件。'
                },
                'AS': {
                    title: '角边条件（角和非对应边）',
                    success: '这种情况理论上不会成功，如果出现了可能是程序问题哦。',
                    failure: '知道一个角和一条不相关的边，信息不足以确定三角形的形状。'
                }
            };
            
            const info = explanations[condition];
            if (!info) {
                // 兜底文案
                return {
                    title: '未知条件',
                    description: isSuccess 
                        ? '这是一个特殊的条件组合，能够确定三角形的形状！'
                        : '这个条件组合不足以确定唯一的三角形形状，需要更多信息。'
                };
            }
            
            return {
                title: info.title,
                description: isSuccess ? info.success : info.failure
            };
        }
        
        // 保存探索记录到localStorage
        function saveExplorationHistory() {
            try {
                // 将Set转换为数组进行存储
                const successArray = Array.from(successfulConditions);
                const failureArray = Array.from(failedConditions);
                
                localStorage.setItem(STORAGE_KEY_SUCCESS, JSON.stringify(successArray));
                localStorage.setItem(STORAGE_KEY_FAILURE, JSON.stringify(failureArray));
                
                console.log('探索记录已保存到localStorage');
            } catch (error) {
                console.warn('保存探索记录失败:', error);
            }
        }
        
        // 从localStorage加载探索记录
        function loadExplorationHistory() {
            try {
                // 加载成功条件
                const successData = localStorage.getItem(STORAGE_KEY_SUCCESS);
                if (successData) {
                    const successArray = JSON.parse(successData);
                    successfulConditions = new Set(successArray);
                }
                
                // 加载失败条件
                const failureData = localStorage.getItem(STORAGE_KEY_FAILURE);
                if (failureData) {
                    const failureArray = JSON.parse(failureData);
                    failedConditions = new Set(failureArray);
                }
                
                // 更新历史显示
                updateHistoryDisplay();
                
                console.log('探索记录已从localStorage加载');
            } catch (error) {
                console.warn('加载探索记录失败:', error);
                // 如果加载失败，初始化为空的Set
                successfulConditions = new Set();
                failedConditions = new Set();
            }
        }
        
        // 清除localStorage中的探索记录
        function clearExplorationHistory() {
            try {
                localStorage.removeItem(STORAGE_KEY_SUCCESS);
                localStorage.removeItem(STORAGE_KEY_FAILURE);
                console.log('localStorage中的探索记录已清除');
            } catch (error) {
                console.warn('清除探索记录失败:', error);
            }
        }
        
        // 重新开始教学
        function restartTeaching() {
            // 显示自定义确认对话框
            showCustomConfirm();
        }
        
        // 显示自定义确认对话框
        function showCustomConfirm() {
            const confirmOverlay = document.getElementById('custom-confirm');
            confirmOverlay.style.display = 'flex';
            
            // 添加事件监听器
            document.getElementById('confirm-cancel').onclick = hideCustomConfirm;
            document.getElementById('confirm-ok').onclick = function() {
                hideCustomConfirm();
                executeRestart();
            };
            
            // ESC键关闭
            const escHandler = function(e) {
                if (e.key === 'Escape') {
                    hideCustomConfirm();
                    document.removeEventListener('keydown', escHandler);
                }
            };
            document.addEventListener('keydown', escHandler);
            
            // 点击背景关闭
            confirmOverlay.onclick = function(e) {
                if (e.target === confirmOverlay) {
                    hideCustomConfirm();
                }
            };
        }
        
        // 隐藏自定义确认对话框
        function hideCustomConfirm() {
            const confirmOverlay = document.getElementById('custom-confirm');
            confirmOverlay.style.display = 'none';
            
            // 清除事件监听器
            document.getElementById('confirm-cancel').onclick = null;
            document.getElementById('confirm-ok').onclick = null;
            confirmOverlay.onclick = null;
        }
        
        // 执行重新开始操作
        function executeRestart() {
            // 清除探索记录
            successfulConditions.clear();
            failedConditions.clear();
            
            // 清除localStorage
            clearExplorationHistory();
            
            // 重置三角形（这会清除所有状态）
            resetTriangle();
            
            // 更新历史显示
            updateHistoryDisplay();
            
            // 显示成功提示
            alert('✅ 教学已重新开始！\n\n所有探索记录和状态已清除，可以开始新的教学了。');
            
            console.log('教学已重新开始，所有记录已清除');
        }
        
        // 页面加载完成后初始化
        window.addEventListener('load', init);
    </script>
</body>
</html>
