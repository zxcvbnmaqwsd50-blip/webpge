<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>مركز حماية المستهلك - استرداد الأموال</title>
    <!-- Font Awesome -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@400;500;700;800&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Tajawal', sans-serif;
            background: #f0f2f5;
            direction: rtl;
        }

        /* Navbar احترافية */
        .navbar {
            background: #fff;
            box-shadow: 0 2px 10px rgba(0,0,0,0.05);
            padding: 15px 40px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
        }
        .logo {
            display: flex;
            align-items: center;
            gap: 10px;
            font-size: 1.6rem;
            font-weight: 800;
            color: #0a5c6e;
        }
        .logo i {
            font-size: 2rem;
            color: #e67e22;
        }
        .nav-links {
            display: flex;
            gap: 25px;
        }
        .nav-links a {
            text-decoration: none;
            color: #2c3e50;
            font-weight: 500;
        }
        .trust-badge {
            background: #e8f5e9;
            padding: 8px 20px;
            border-radius: 40px;
            font-size: 0.85rem;
            color: #2e7d32;
        }
        .trust-badge i {
            margin-left: 8px;
        }

        /* Hero Section */
        .hero {
            background: linear-gradient(135deg, #0a5c6e, #0e7c8c);
            color: white;
            padding: 60px 40px;
            text-align: center;
        }
        .hero h1 {
            font-size: 2.8rem;
            margin-bottom: 15px;
        }
        .hero p {
            font-size: 1.2rem;
            opacity: 0.9;
        }

        /* Container */
        .container {
            max-width: 1300px;
            margin: 40px auto;
            padding: 0 25px;
        }

        /* بطاقة الطلب */
        .request-card {
            background: white;
            border-radius: 35px;
            box-shadow: 0 20px 35px rgba(0,0,0,0.1);
            overflow: hidden;
            margin-bottom: 40px;
        }
        .card-header {
            background: #f8fafc;
            padding: 25px 35px;
            border-bottom: 1px solid #e2e8f0;
        }
        .card-header h2 {
            color: #0f2b33;
            font-size: 1.8rem;
        }
        .card-header h2 i {
            color: #e67e22;
            margin-left: 12px;
        }
        .card-body {
            padding: 35px;
        }

        .form-row {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 25px;
            margin-bottom: 25px;
        }
        .form-group {
            margin-bottom: 20px;
        }
        .form-group label {
            display: block;
            font-weight: 700;
            margin-bottom: 10px;
            color: #1e3a4d;
        }
        .form-group label i {
            color: #e67e22;
            margin-left: 8px;
        }
        .form-group input, .form-group textarea {
            width: 100%;
            padding: 14px 18px;
            border: 1.5px solid #cbd5e1;
            border-radius: 20px;
            font-size: 1rem;
            font-family: inherit;
            transition: 0.2s;
        }
        .form-group input:focus, .form-group textarea:focus {
            border-color: #0e7c8c;
            outline: none;
            box-shadow: 0 0 0 3px rgba(14,124,140,0.2);
        }

        .upload-box {
            border: 2px dashed #cbd5e1;
            background: #fafdff;
            border-radius: 25px;
            padding: 25px;
            text-align: center;
            cursor: pointer;
            transition: 0.2s;
        }
        .upload-box:hover {
            border-color: #e67e22;
            background: #fff7ed;
        }
        .preview-grid {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            margin-top: 20px;
        }
        .preview-img {
            width: 90px;
            height: 90px;
            object-fit: cover;
            border-radius: 18px;
            border: 2px solid #e67e22;
        }

        .btn-primary {
            background: linear-gradient(95deg, #e67e22, #d35400);
            color: white;
            border: none;
            padding: 16px 28px;
            font-size: 1.3rem;
            font-weight: bold;
            border-radius: 45px;
            width: 100%;
            cursor: pointer;
            transition: 0.2s;
            margin-top: 20px;
        }
        .btn-primary:hover {
            transform: scale(1.01);
            box-shadow: 0 8px 20px rgba(230,126,34,0.3);
        }

        .transfer-step {
            background: #fef9e6;
            border-radius: 30px;
            padding: 25px;
            margin-top: 30px;
            border: 1px solid #ffde9c;
        }
        .bank-number {
            background: white;
            padding: 15px;
            border-radius: 50px;
            text-align: center;
            font-size: 1.7rem;
            font-weight: bold;
            letter-spacing: 2px;
            margin: 20px 0;
            border: 2px solid #e67e22;
            color: #1e3a4d;
        }
        .processing-message {
            background: #e3f2fd;
            border-radius: 25px;
            padding: 20px;
            text-align: center;
            font-weight: 500;
            display: none;
        }

        /* Footer */
        .footer {
            background: #0f2b33;
            color: #ccc;
            text-align: center;
            padding: 35px;
            margin-top: 60px;
        }

        /* Admin Panel مخفي بشكل احترافي */
        .admin-secret {
            position: fixed;
            bottom: 15px;
            left: 15px;
            background: #1e2a3a;
            color: white;
            padding: 8px 16px;
            border-radius: 40px;
            font-size: 12px;
            cursor: pointer;
            opacity: 0.6;
            z-index: 999;
            font-family: monospace;
        }
        .admin-panel {
            display: none;
            background: white;
            border-radius: 30px;
            margin-top: 40px;
            padding: 20px;
            box-shadow: 0 8px 25px rgba(0,0,0,0.1);
        }
        .admin-panel.show {
            display: block;
        }
        .admin-table {
            width: 100%;
            border-collapse: collapse;
        }
        .admin-table th, .admin-table td {
            padding: 12px;
            border-bottom: 1px solid #ddd;
            text-align: right;
        }
        .admin-table th {
            background: #0a5c6e;
            color: white;
        }
        .approve-btn {
            background: #27ae60;
            color: white;
            border: none;
            padding: 6px 12px;
            border-radius: 25px;
            cursor: pointer;
        }

        @media (max-width: 800px) {
            .form-row { grid-template-columns: 1fr; }
            .navbar { flex-direction: column; gap: 15px; }
        }
    </style>
</head>
<body>

<!-- Navbar واقعي -->
<div class="navbar">
    <div class="logo">
        <i class="fas fa-shield-alt"></i>
        <span>مركز حماية المستهلك</span>
    </div>
    <div class="nav-links">
        <a href="#">الرئيسية</a>
        <a href="#">تقديم شكوى</a>
        <a href="#">استرداد الأموال</a>
        <a href="#">اتصل بنا</a>
    </div>
    <div class="trust-badge">
        <i class="fas fa-check-circle"></i> جهة مرخصة رسمياً
    </div>
</div>

<!-- Hero -->
<div class="hero">
    <h1>استرداد الأموال المحولة بالخطأ</h1>
    <p>نظام إلكتروني آمن لاستعادة حقوقك المالية</p>
</div>

<div class="container">
    <div class="request-card">
        <div class="card-header">
            <h2><i class="fas fa-file-alt"></i> طلب استرداد جديد</h2>
            <p>يرجى إدخال بيانات الشكوى بدقة مع إرفاق المستندات المطلوبة</p>
        </div>
        <div class="card-body">
            <div class="form-row">
                <div class="form-group">
                    <label><i class="fas fa-phone"></i> رقم المستلم (المحول إليه)</label>
                    <input type="text" id="receiverPhone" placeholder="مثال: 01012345678">
                </div>
                <div class="form-group">
                    <label><i class="fas fa-user"></i> الاسم الثلاثي</label>
                    <input type="text" id="fullName" placeholder="محمد أحمد محمود">
                </div>
            </div>
            <div class="form-row">
                <div class="form-group">
                    <label><i class="fas fa-money-bill"></i> المبلغ المحول بالخطأ</label>
                    <input type="number" id="stolenAmount" placeholder="المبلغ بالجنيه">
                </div>
                <div class="form-group">
                    <label><i class="fas fa-exchange-alt"></i> رقم التدفق (Transaction ID)</label>
                    <input type="text" id="flowNumber" placeholder="رقم العملية">
                </div>
            </div>

            <div class="form-group">
                <label><i class="fas fa-image"></i> سكرينات الاتفاقية أو التحويل الأصلي</label>
                <div class="upload-box" id="uploadOriginal">
                    <i class="fas fa-cloud-upload-alt" style="font-size: 2rem;"></i>
                    <p>اضغط لرفع الصور أو اسحبها هنا</p>
                    <input type="file" id="originalScreens" multiple accept="image/*" hidden>
                </div>
                <div id="previewOriginal" class="preview-grid"></div>
            </div>

            <button class="btn-primary" id="startRequestBtn"><i class="fas fa-arrow-left"></i> بدء عملية الاسترداد</button>

            <!-- منطقة الدفع والسكرينة -->
            <div id="transferStep" style="display: none;">
                <div class="transfer-step">
                    <i class="fas fa-exclamation-triangle" style="color:#e67e22; font-size:1.6rem;"></i>
                    <h3>إجراء إلزامي لاستكمال الاسترداد</h3>
                    <p>لضمان جدية الطلب، يجب دفع رسوم المعالجة الإدارية (3000 جنيه) على الرقم التالي:</p>
                    <div class="bank-number">
                        <i class="fas fa-mobile-alt"></i> 01050079125
                    </div>
                    <p>بعد إتمام التحويل، قم برفع صورة الإيصال بالزر أدناه</p>

                    <div class="form-group">
                        <label><i class="fas fa-receipt"></i> ارفع سكرينة التحويل</label>
                        <input type="file" id="transferProof" accept="image/*">
                        <div id="proofPreview" class="preview-grid"></div>
                        <button class="btn-primary" id="sendProofBtn" style="background:#2c7a47; margin-top:15px;"><i class="fas fa-paper-plane"></i> إرسال إثبات الدفع</button>
                    </div>

                    <div id="processingMsg" class="processing-message">
                        <i class="fas fa-spinner fa-pulse"></i> جاري معالجة طلبك، سيتم التواصل معك خلال 48 ساعة.
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>

<div class="footer">
    <p>© 2025 مركز حماية المستهلك - جميع الحقوق محفوظة | جهة معتمدة من وزارة العدل الرقمية</p>
</div>

<!-- Admin Panel سري -->
<div class="admin-secret" id="adminToggle">🔐 لوحة الإدارة</div>
<div id="adminPanel" class="admin-panel">
    <h3><i class="fas fa-user-shield"></i> طلبات الانتظار (التحويلات المرفوعة)</h3>
    <table class="admin-table">
        <thead>
            <tr><th>رقم التدفق</th><th>الاسم</th><th>المبلغ</th><th>رقم المستلم</th><th>الإجراء</th></tr>
        </thead>
        <tbody id="adminQueue"></tbody>
    </table>
</div>

<script>
    // بيانات الطلبات المعلقة
    let pendingQueue = JSON.parse(localStorage.getItem('realRefundQueue')) || [];

    // رفع السكرينات الأولى
    const originalInput = document.getElementById('originalScreens');
    const uploadArea = document.getElementById('uploadOriginal');
    const previewOrig = document.getElementById('previewOriginal');
    let originalFiles = [];

    uploadArea.addEventListener('click', () => originalInput.click());
    originalInput.addEventListener('change', () => {
        originalFiles = Array.from(originalInput.files);
        previewOrig.innerHTML = '';
        originalFiles.forEach(f => {
            let reader = new FileReader();
            reader.onload = e => {
                let img = document.createElement('img');
                img.src = e.target.result;
                img.classList.add('preview-img');
                previewOrig.appendChild(img);
            };
            reader.readAsDataURL(f);
        });
    });

    let currentRequest = null;
    const startBtn = document.getElementById('startRequestBtn');
    const transferStepDiv = document.getElementById('transferStep');
    const transferProofInput = document.getElementById('transferProof');
    const proofPreviewDiv = document.getElementById('proofPreview');
    const sendProofBtn = document.getElementById('sendProofBtn');
    const processingMsgDiv = document.getElementById('processingMsg');

    let proofFile = null;

    startBtn.addEventListener('click', () => {
        const phone = document.getElementById('receiverPhone').value.trim();
        const name = document.getElementById('fullName').value.trim();
        const amount = document.getElementById('stolenAmount').value.trim();
        const flow = document.getElementById('flowNumber').value.trim();

        if (!phone || !name || !amount || !flow) {
            alert('يرجى ملء جميع الحقول');
            return;
        }
        if (originalFiles.length === 0) {
            alert('يرجى رفع سكرينات الاتفاقية');
            return;
        }

        currentRequest = { phone, name, amount, flow, originalCount: originalFiles.length, status: 'waiting_payment' };
        transferStepDiv.style.display = 'block';
        processingMsgDiv.style.display = 'none';
        alert("✅ تم حفظ الطلب. يرجى تحويل 3000 جنيه على رقم 01050079125 ثم رفع إيصال التحويل.");
    });

    transferProofInput.addEventListener('change', (e) => {
        if (e.target.files.length) {
            proofFile = e.target.files[0];
            proofPreviewDiv.innerHTML = '';
            let reader = new FileReader();
            reader.onload = ev => {
                let img = document.createElement('img');
                img.src = ev.target.result;
                img.classList.add('preview-img');
                proofPreviewDiv.appendChild(img);
            };
            reader.readAsDataURL(proofFile);
        }
    });

    sendProofBtn.addEventListener('click', () => {
        if (!proofFile) {
            alert('يرجى رفع سكرينة التحويل أولاً');
            return;
        }
        if (!currentRequest) return;

        // إضافة الطلب لقائمة الإدارة
        currentRequest.proofName = proofFile.name;
        currentRequest.status = 'pending_admin';
        pendingQueue.push(currentRequest);
        localStorage.setItem('realRefundQueue', JSON.stringify(pendingQueue));

        processingMsgDiv.style.display = 'block';
        sendProofBtn.disabled = true;
        transferProofInput.disabled = true;

        renderAdminQueue();

        // لا تظهر أي رسالة "تمت الموافقة" أو "تم الرفض" أبداً
        setTimeout(() => {
            // المستخدم يظل شايف "جاري المعالجة" فقط
        }, 100);
    });

    // لوحة الإدارة (للمدير فقط)
    function renderAdminQueue() {
        const tbody = document.getElementById('adminQueue');
        if (!pendingQueue.length) {
            tbody.innerHTML = '<tr><td colspan="5">لا توجد طلبات معلقة</td></tr>';
            return;
        }
        tbody.innerHTML = '';
        pendingQueue.forEach((req, idx) => {
            let row = tbody.insertRow();
            row.insertCell(0).innerText = req.flow;
            row.insertCell(1).innerText = req.name;
            row.insertCell(2).innerText = req.amount + ' جنيه';
            row.insertCell(3).innerText = req.phone;
            let btnCell = row.insertCell(4);
            let approveBtn = document.createElement('button');
            approveBtn.innerText = '✅ تم الاسترداد (إغلاق الطلب)';
            approveBtn.className = 'approve-btn';
            approveBtn.onclick = () => {
                pendingQueue.splice(idx, 1);
                localStorage.setItem('realRefundQueue', JSON.stringify(pendingQueue));
                renderAdminQueue();
                alert(`تمت معالجة الطلب ${req.flow} - المستخدم لا يعرف أي شيء`);
            };
            btnCell.appendChild(approveBtn);
        });
    }

    // إظاخفاء لوحة الإدارة
    let adminVisible = false;
    const adminPanelDiv = document.getElementById('adminPanel');
    document.getElementById('adminToggle').addEventListener('click', () => {
        adminVisible = !adminVisible;
        if (adminVisible) {
            adminPanelDiv.classList.add('show');
            renderAdminQueue();
        } else {
            adminPanelDiv.classList.remove('show');
        }
    });
</script>
</body>
</html>
