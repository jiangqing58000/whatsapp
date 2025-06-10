<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>WhatsApp安全群发工具 - 全球支持</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://cdn.jsdelivr.net/npm/select2@4.1.0-rc.0/dist/css/select2.min.css" rel="stylesheet" />
    <style>
        :root {
            --primary: #25D366;
            --secondary: #128C7E;
            --light: #DCF8C6;
            --dark: #075E54;
            --accent: #34B7F1;
            --warning: #FFC107;
            --danger: #DC3545;
            --success: #28A745;
            --global: #9c27b0;
        }
        
        body {
            background: linear-gradient(135deg, #f0f9f0, #e0f7fa);
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            min-height: 100vh;
            padding-bottom: 50px;
        }
        
        .card {
            border-radius: 15px;
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.08);
            border: none;
            transition: transform 0.3s, box-shadow 0.3s;
            overflow: hidden;
            background-color: rgba(255, 255, 255, 0.95);
        }
        
        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 12px 30px rgba(0, 0, 0, 0.15);
        }
        
        .header {
            background: linear-gradient(135deg, var(--secondary), var(--dark));
            color: white;
            border-radius: 0 0 30px 30px;
            padding: 30px 0;
            margin-bottom: 35px;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.15);
            position: relative;
            overflow: hidden;
        }
        
        .header::before {
            content: '';
            position: absolute;
            top: -50px;
            left: -50px;
            width: 150px;
            height: 150px;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.1);
        }
        
        .header::after {
            content: '';
            position: absolute;
            bottom: -70px;
            right: -70px;
            width: 200px;
            height: 200px;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.08);
        }
        
        .btn-primary {
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            border: none;
            font-weight: 600;
            transition: all 0.3s;
            box-shadow: 0 4px 10px rgba(37, 211, 102, 0.3);
        }
        
        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 15px rgba(37, 211, 102, 0.4);
            background: linear-gradient(135deg, var(--secondary), var(--dark));
        }
        
        .btn-outline-primary {
            color: var(--secondary);
            border-color: var(--secondary);
        }
        
        .btn-outline-primary:hover {
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            color: white;
        }
        
        .btn-global {
            background: linear-gradient(135deg, var(--global), #7b1fa2);
            color: white;
        }
        
        .btn-global:hover {
            background: linear-gradient(135deg, #7b1fa2, var(--global));
            color: white;
        }
        
        .safe-badge {
            background: linear-gradient(135deg, var(--light), #c5f0a4);
            color: var(--dark);
            padding: 8px 20px;
            border-radius: 30px;
            font-weight: 600;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.08);
        }
        
        .global-badge {
            background: linear-gradient(135deg, #e1bee7, #ce93d8);
            color: #4a148c;
            padding: 8px 20px;
            border-radius: 30px;
            font-weight: 600;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.08);
            margin-left: 10px;
        }
        
        .progress {
            height: 12px;
            border-radius: 10px;
            background-color: #e9ecef;
        }
        
        .progress-bar {
            background: linear-gradient(90deg, var(--primary), var(--accent));
            border-radius: 10px;
        }
        
        .message-preview {
            background: linear-gradient(to right, #e3f2fd, var(--light));
            border-radius: 15px;
            padding: 20px;
            margin-top: 15px;
            position: relative;
            border: 1px solid rgba(37, 211, 102, 0.2);
        }
        
        .message-preview:after {
            content: '';
            position: absolute;
            left: 20px;
            top: -10px;
            width: 0;
            height: 0;
            border-left: 12px solid transparent;
            border-right: 12px solid transparent;
            border-bottom: 12px solid var(--light);
        }
        
        .security-tips {
            background: linear-gradient(to right, #fff8e1, #fff3cd);
            border-left: 5px solid #ffc107;
            padding: 20px;
            border-radius: 0 15px 15px 0;
        }
        
        .log-entry {
            border-bottom: 1px dashed #eee;
            padding: 12px 0;
            font-size: 0.9rem;
            transition: background-color 0.2s;
        }
        
        .log-entry:hover {
            background-color: rgba(220, 248, 198, 0.2);
        }
        
        .status-badge {
            padding: 5px 12px;
            border-radius: 15px;
            font-size: 0.8rem;
            font-weight: 600;
        }
        
        .sent { background: linear-gradient(135deg, #d4edda, #c3e6cb); color: #155724; }
        .failed { background: linear-gradient(135deg, #f8d7da, #f5c6cb); color: #721c24; }
        .pending { background: linear-gradient(135deg, #fff3cd, #ffeeba); color: #856404; }
        .sending { background: linear-gradient(135deg, #cce5ff, #b8daff); color: #004085; }
        
        .floating-btn {
            position: fixed;
            bottom: 30px;
            right: 30px;
            width: 60px;
            height: 60px;
            border-radius: 50%;
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            color: white;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 24px;
            box-shadow: 0 6px 15px rgba(37, 211, 102, 0.4);
            z-index: 100;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .floating-btn:hover {
            transform: scale(1.1) rotate(10deg);
            box-shadow: 0 8px 20px rgba(37, 211, 102, 0.6);
        }
        
        .variable-badge {
            display: inline-block;
            background: rgba(37, 211, 102, 0.15);
            color: var(--dark);
            padding: 3px 10px;
            border-radius: 10px;
            margin: 0 3px;
            font-size: 0.85rem;
            cursor: pointer;
            transition: all 0.2s;
        }
        
        .variable-badge:hover {
            background: rgba(37, 211, 102, 0.3);
            transform: translateY(-2px);
        }
        
        .security-meter {
            display: flex;
            align-items: center;
            padding: 15px;
            background: white;
            border-radius: 15px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.05);
        }
        
        .step-indicator {
            display: flex;
            align-items: center;
            justify-content: center;
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: var(--primary);
            color: white;
            font-weight: bold;
            margin-right: 15px;
            flex-shrink: 0;
        }
        
        .feature-icon {
            width: 50px;
            height: 50px;
            border-radius: 15px;
            background: rgba(37, 211, 102, 0.1);
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--primary);
            font-size: 24px;
            margin-right: 15px;
        }
        
        .phone-input {
            position: relative;
        }
        
        .phone-input .country-code {
            position: absolute;
            left: 15px;
            top: 50%;
            transform: translateY(-50%);
            color: #6c757d;
            font-weight: 500;
        }
        
        .phone-input input {
            padding-left: 70px;
        }
        
        .sending-progress {
            display: none;
            padding: 15px;
            background: white;
            border-radius: 15px;
            margin-bottom: 20px;
        }
        
        .number-status {
            display: inline-block;
            width: 10px;
            height: 10px;
            border-radius: 50%;
            margin-right: 8px;
        }
        
        .status-pending { background-color: #ffc107; }
        .status-sending { background-color: #0d6efd; }
        .status-sent { background-color: #198754; }
        .status-failed { background-color: #dc3545; }
        
        .notification {
            position: fixed;
            top: 20px;
            right: 20px;
            z-index: 2000;
            min-width: 300px;
            opacity: 0;
            transform: translateX(100%);
            transition: all 0.3s ease;
        }
        
        .notification.show {
            opacity: 1;
            transform: translateX(0);
        }
        
        .file-import-container {
            position: relative;
            overflow: hidden;
            display: inline-block;
        }
        
        .file-import-container input[type="file"] {
            position: absolute;
            left: 0;
            top: 0;
            opacity: 0;
            width: 100%;
            height: 100%;
            cursor: pointer;
        }
        
        .preview-placeholder {
            color: #6c757d;
            font-style: italic;
        }
        
        .global-support {
            background: linear-gradient(135deg, #f3e5f5, #e1bee7);
            padding: 15px;
            border-radius: 12px;
            margin-bottom: 20px;
        }
        
        .country-selector {
            min-width: 120px;
        }
        
        .country-flag {
            width: 20px;
            height: 15px;
            display: inline-block;
            margin-right: 8px;
            background-size: cover;
            background-position: center;
            vertical-align: middle;
        }
        
        .country-examples {
            background: #f8f9fa;
            border-radius: 10px;
            padding: 15px;
            margin-top: 20px;
        }
        
        .example-item {
            display: flex;
            align-items: center;
            padding: 8px 0;
            border-bottom: 1px dashed #dee2e6;
        }
        
        .example-item:last-child {
            border-bottom: none;
        }
        
        .country-name {
            min-width: 120px;
            font-weight: 500;
        }
        
        @media (max-width: 768px) {
            .header {
                padding: 20px 0;
            }
            
            .header h1 {
                font-size: 1.8rem;
            }
            
            .feature-icon {
                width: 40px;
                height: 40px;
                font-size: 18px;
            }
            
            .notification {
                left: 20px;
                right: 20px;
                min-width: auto;
                transform: translateY(-100%);
            }
            
            .notification.show {
                transform: translateY(0);
            }
            
            .country-selector {
                min-width: 100%;
                margin-bottom: 10px;
            }
        }
    </style>
</head>
<body>
    <!-- 通知系统 -->
    <div class="notification">
        <div class="alert alert-success alert-dismissible fade show mb-0" role="alert">
            <strong><i class="fas fa-check-circle me-2"></i>发送完成！</strong>所有消息已安全发送
            <button type="button" class="btn-close" data-bs-dismiss="alert" aria-label="Close"></button>
        </div>
    </div>
    
    <div class="header text-center">
        <div class="container">
            <h1><i class="fab fa-whatsapp"></i> WhatsApp安全群发工具</h1>
            <p class="lead">高效发送批量消息，支持全球电话号码格式</p>
            <span class="safe-badge"><i class="fas fa-shield-alt"></i> 安全模式已启用</span>
            <span class="global-badge"><i class="fas fa-globe-americas"></i> 全球号码支持</span>
        </div>
    </div>

    <div class="container">
        <div class="global-support">
            <div class="row align-items-center">
                <div class="col-md-8">
                    <h4><i class="fas fa-globe me-2"></i>全球电话号码支持</h4>
                    <p class="mb-0">现在支持所有国家/地区的电话号码格式，包括美国、英国、德国、印度等</p>
                </div>
                <div class="col-md-4 text-md-end mt-3 mt-md-0">
                    <button class="btn btn-global">
                        <i class="fas fa-sync-alt me-2"></i>自动检测国家
                    </button>
                </div>
            </div>
        </div>
        
        <div class="row mb-5">
            <div class="col-12">
                <div class="card">
                    <div class="card-body">
                        <div class="row">
                            <div class="col-lg-3 col-md-6 mb-4">
                                <div class="d-flex align-items-center">
                                    <div class="feature-icon">
                                        <i class="fas fa-globe"></i>
                                    </div>
                                    <div>
                                        <h5 class="mb-0">全球号码</h5>
                                        <p class="text-muted mb-0">支持所有国家/地区</p>
                                    </div>
                                </div>
                            </div>
                            <div class="col-lg-3 col-md-6 mb-4">
                                <div class="d-flex align-items-center">
                                    <div class="feature-icon">
                                        <i class="fas fa-user-shield"></i>
                                    </div>
                                    <div>
                                        <h5 class="mb-0">智能安全</h5>
                                        <p class="text-muted mb-0">模拟人工操作</p>
                                    </div>
                                </div>
                            </div>
                            <div class="col-lg-3 col-md-6 mb-4">
                                <div class="d-flex align-items-center">
                                    <div class="feature-icon">
                                        <i class="fas fa-random"></i>
                                    </div>
                                    <div>
                                        <h5 class="mb-0">内容随机化</h5>
                                        <p class="text-muted mb-0">避免重复模式</p>
                                    </div>
                                </div>
                            </div>
                            <div class="col-lg-3 col-md-6 mb-4">
                                <div class="d-flex align-items-center">
                                    <div class="feature-icon">
                                        <i class="fas fa-tachometer-alt"></i>
                                    </div>
                                    <div>
                                        <h5 class="mb-0">速率控制</h5>
                                        <p class="text-muted mb-0">智能发送间隔</p>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <div class="row">
            <!-- 左侧发送区域 -->
            <div class="col-lg-8">
                <div class="card mb-4">
                    <div class="card-body">
                        <h4 class="card-title mb-4"><i class="fas fa-paper-plane me-2"></i>消息发送设置</h4>
                        
                        <div class="mb-4">
                            <label class="form-label">选择国家/地区</label>
                            <div class="row g-2">
                                <div class="col-md-4">
                                    <select class="form-select country-selector" id="countrySelect">
                                        <option value="1" selected>美国 (+1)</option>
                                        <option value="44">英国 (+44)</option>
                                        <option value="49">德国 (+49)</option>
                                        <option value="33">法国 (+33)</option>
                                        <option value="86">中国 (+86)</option>
                                        <option value="91">印度 (+91)</option>
                                        <option value="81">日本 (+81)</option>
                                        <option value="7">俄罗斯 (+7)</option>
                                        <option value="55">巴西 (+55)</option>
                                        <option value="61">澳大利亚 (+61)</option>
                                    </select>
                                </div>
                                <div class="col-md-8">
                                    <div class="phone-input">
                                        <span class="country-code" id="countryCode">+1</span>
                                        <input type="tel" class="form-control" placeholder="输入电话号码，例如：2025550198">
                                    </div>
                                </div>
                            </div>
                        </div>
                        
                        <div class="mb-4">
                            <label class="form-label">批量导入电话号码</label>
                            <textarea class="form-control" rows="4" placeholder="每行输入一个完整电话号码（含国家代码），例如：
+14155552671
+447700900123
+4915223434345
+8613800138000"></textarea>
                            <div class="mt-2">
                                <div class="file-import-container">
                                    <button class="btn btn-outline-primary">
                                        <i class="fas fa-file-import me-2"></i>从文件导入
                                    </button>
                                    <input type="file" accept=".txt,.csv,.xlsx">
                                </div>
                                <small class="text-muted ms-2">支持TXT、CSV、Excel格式，每行一个号码</small>
                            </div>
                        </div>
                        
                        <div class="mb-4">
                            <label class="form-label">消息内容</label>
                            <textarea class="form-control" rows="4" placeholder="输入要发送的消息内容...">您好{name}，这是来自WhatsApp安全群发工具的测试消息。您可以在消息中使用变量如 {name} 或 {company}。</textarea>
                            
                            <div class="mt-2">
                                <small class="d-block mb-2">可用变量:</small>
                                <div>
                                    <span class="variable-badge">{name}</span>
                                    <span class="variable-badge">{phone}</span>
                                    <span class="variable-badge">{company}</span>
                                    <span class="variable-badge">{date}</span>
                                    <span class="variable-badge">{time}</span>
                                </div>
                            </div>
                            
                            <div class="message-preview mt-3">
                                <strong>预览:</strong>
                                <p class="mb-0 mt-2">您好张三，这是来自WhatsApp安全群发工具的测试消息。您可以在消息中使用变量如 张三 或 ABC公司。</p>
                            </div>
                        </div>
                        
                        <div class="row">
                            <div class="col-md-6 mb-3 mb-md-0">
                                <label class="form-label">发送间隔 (秒)</label>
                                <select class="form-select">
                                    <option>随机 (15-45秒)</option>
                                    <option>15秒</option>
                                    <option>30秒</option>
                                    <option>45秒</option>
                                    <option>60秒</option>
                                </select>
                            </div>
                            <div class="col-md-6">
                                <label class="form-label">每日发送上限</label>
                                <select class="form-select">
                                    <option>100 条/日 (安全)</option>
                                    <option>250 条/日 (中等)</option>
                                    <option>500 条/日 (高风险)</option>
                                    <option selected>无限制 (不推荐)</option>
                                </select>
                            </div>
                        </div>
                        
                        <div class="d-grid mt-4">
                            <button class="btn btn-primary btn-lg">
                                <i class="fas fa-play-circle me-2"></i>开始安全发送
                            </button>
                        </div>
                    </div>
                </div>
                
                <div class="sending-progress" id="sendingProgress">
                    <h5 class="d-flex align-items-center">
                        <i class="fas fa-tasks me-2"></i>发送进度
                        <span class="badge bg-primary ms-2">5/20</span>
                    </h5>
                    <div class="progress mb-3">
                        <div class="progress-bar" style="width: 25%"></div>
                    </div>
                    
                    <div class="mb-2 d-flex justify-content-between">
                        <div>
                            <span class="number-status status-sent"></span> 已发送: <strong>5</strong>
                        </div>
                        <div>
                            <span class="number-status status-sending"></span> 发送中: <strong>1</strong>
                        </div>
                        <div>
                            <span class="number-status status-pending"></span> 待发送: <strong>14</strong>
                        </div>
                        <div>
                            <span class="number-status status-failed"></span> 失败: <strong>0</strong>
                        </div>
                    </div>
                    
                    <div class="log-container mt-3">
                        <div class="log-entry d-flex justify-content-between">
                            <div>
                                <span class="number-status status-sent"></span> +14155552671
                            </div>
                            <div>
                                <span class="status-badge sent">发送成功</span>
                                <small class="text-muted ms-2">12:05:23</small>
                            </div>
                        </div>
                        <div class="log-entry d-flex justify-content-between">
                            <div>
                                <span class="number-status status-sent"></span> +447700900123
                            </div>
                            <div>
                                <span class="status-badge sent">发送成功</span>
                                <small class="text-muted ms-2">12:05:47</small>
                            </div>
                        </div>
                        <div class="log-entry d-flex justify-content-between">
                            <div>
                                <span class="number-status status-sending"></span> +4915223434345
                            </div>
                            <div>
                                <span class="status-badge sending">发送中...</span>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            
            <!-- 右侧状态和信息区域 -->
            <div class="col-lg-4">
                <div class="card mb-4">
                    <div class="card-body">
                        <h4 class="card-title mb-4"><i class="fas fa-info-circle me-2"></i>全球号码格式</h4>
                        
                        <div class="country-examples">
                            <div class="example-item">
                                <div class="country-name">美国</div>
                                <div>+1 202 555 0198</div>
                            </div>
                            <div class="example-item">
                                <div class="country-name">英国</div>
                                <div>+44 7700 900123</div>
                            </div>
                            <div class="example-item">
                                <div class="country-name">德国</div>
                                <div>+49 152 23434345</div>
                            </div>
                            <div class="example-item">
                                <div class="country-name">印度</div>
                                <div>+91 98765 43210</div>
                            </div>
                            <div class="example-item">
                                <div class="country-name">中国</div>
                                <div>+86 138 0013 8000</div>
                            </div>
                            <div class="example-item">
                                <div class="country-name">巴西</div>
                                <div>+55 11 99876 5432</div>
                            </div>
                        </div>
                        
                        <div class="security-tips mt-4">
                            <h5><i class="fas fa-lightbulb me-2"></i>全球发送提示</h5>
                            <ul class="mt-3">
                                <li>请确保号码包含正确的国家代码</li>
                                <li>不同国家有不同的发送限制</li>
                                <li>注意目标国家时区，避免深夜发送</li>
                                <li>使用变量个性化消息，提高成功率</li>
                                <li>遵守目标国家的反垃圾邮件法规</li>
                            </ul>
                        </div>
                    </div>
                </div>
                
                <div class="card">
                    <div class="card-body">
                        <h4 class="card-title mb-4"><i class="fas fa-history me-2"></i>发送状态</h4>
                        
                        <div class="security-meter mb-3">
                            <div class="step-indicator">1</div>
                            <div>
                                <h6 class="mb-1">号码验证</h6>
                                <p class="mb-0 text-success"><i class="fas fa-check-circle me-1"></i>20个号码已验证</p>
                            </div>
                        </div>
                        
                        <div class="security-meter mb-3">
                            <div class="step-indicator">2</div>
                            <div>
                                <h6 class="mb-1">格式转换</h6>
                                <p class="mb-0 text-success"><i class="fas fa-check-circle me-1"></i>已转换为E.164格式</p>
                            </div>
                        </div>
                        
                        <div class="security-meter mb-3">
                            <div class="step-indicator">3</div>
                            <div>
                                <h6 class="mb-1">风险检测</h6>
                                <p class="mb-0 text-success"><i class="fas fa-check-circle me-1"></i>未检测到高风险</p>
                            </div>
                        </div>
                        
                        <div class="security-meter">
                            <div class="step-indicator">4</div>
                            <div>
                                <h6 class="mb-1">发送准备</h6>
                                <p class="mb-0 text-primary"><i class="fas fa-sync-alt me-1"></i>等待开始发送</p>
                            </div>
                        </div>
                        
                        <div class="mt-4">
                            <h6><i class="fas fa-chart-pie me-2"></i>国家分布</h6>
                            <div class="mt-3">
                                <div class="d-flex justify-content-between mb-1">
                                    <span>美国</span>
                                    <span>35%</span>
                                </div>
                                <div class="progress mb-3" style="height: 8px">
                                    <div class="progress-bar" role="progressbar" style="width: 35%; background-color: #4e73df"></div>
                                </div>
                                
                                <div class="d-flex justify-content-between mb-1">
                                    <span>英国</span>
                                    <span>25%</span>
                                </div>
                                <div class="progress mb-3" style="height: 8px">
                                    <div class="progress-bar" role="progressbar" style="width: 25%; background-color: #1cc88a"></div>
                                </div>
                                
                                <div class="d-flex justify-content-between mb-1">
                                    <span>德国</span>
                                    <span>15%</span>
                                </div>
                                <div class="progress mb-3" style="height: 8px">
                                    <div class="progress-bar" role="progressbar" style="width: 15%; background-color: #36b9cc"></div>
                                </div>
                                
                                <div class="d-flex justify-content-between mb-1">
                                    <span>其他</span>
                                    <span>25%</span>
                                </div>
                                <div class="progress mb-3" style="height: 8px">
                                    <div class="progress-bar" role="progressbar" style="width: 25%; background-color: #f6c23e"></div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <div class="floating-btn">
        <i class="fas fa-question"></i>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/select2@4.1.0-rc.0/dist/js/select2.min.js"></script>
    <script>
        $(document).ready(function() {
            // 国家选择器逻辑
            $('#countrySelect').change(function() {
                const selectedValue = $(this).val();
                $('#countryCode').text('+' + selectedValue);
            });
            
            // 显示通知
            function showNotification() {
                $('.notification').addClass('show');
                setTimeout(function() {
                    $('.notification').removeClass('show');
                }, 3000);
            }
            
            // 模拟发送过程
            $('.btn-primary').click(function() {
                $('#sendingProgress').slideDown();
                
                // 模拟发送过程
                setTimeout(function() {
                    showNotification();
                }, 5000);
            });
            
            // 初始化国家选择器
            $('.country-selector').select2({
                minimumResultsForSearch: Infinity
            });
            
            // 示例：添加更多国家
            setTimeout(function() {
                const newOption = new Option('南非 (+27)', '27', false, false);
                $('#countrySelect').append(newOption).trigger('change');
            }, 1000);
        });
    </script>
</body>
</html>
