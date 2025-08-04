<تجريبي2>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>نظام تسجيل الآفات والأمراض النباتية | Pest & Disease Recording System</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf-autotable/3.5.28/jspdf.plugin.autotable.min.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Amiri&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary-color: #27ae60;
            --primary-dark: #219653;
            --secondary-color: #2c3e50;
            --secondary-dark: #1a252f;
            --danger-color: #e74c3c;
            --danger-dark: #c0392b;
            --light-color: #f5f5f5;
            --dark-color: #333;
            --white: #fff;
            --gray: #95a5a6;
            --border-radius: 10px;
            --box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            --transition: all 0.3s ease;
        }
        * {
            box-sizing: border-box;
        }
        body {
            font-family: 'Tajawal', 'Arial', sans-serif;
            margin: 0;
            padding: 0;
            background-color: var(--light-color);
            transition: var(--transition);
            line-height: 1.6;
        }
        .container {
            max-width: 100%;
            margin: 0 auto;
            padding: 15px;
        }
        header {
            background-color: var(--secondary-color);
            color: var(--white);
            padding: 15px 0;
            border-radius: var(--border-radius) var(--border-radius) 0 0;
            margin-bottom: 20px;
            box-shadow: var(--box-shadow);
        }
        .header-content {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 0 15px;
            flex-wrap: wrap;
        }
        h1 {
            margin: 0;
            font-size: 1.5rem;
            font-weight: 700;
        }
        .lang-switcher {
            display: flex;
            gap: 8px;
            margin-top: 10px;
        }
        .btn {
            padding: 12px 20px;
            background-color: var(--primary-color);
            color: var(--white);
            border: none;
            border-radius: var(--border-radius);
            cursor: pointer;
            font-size: 1rem;
            font-weight: 500;
            transition: var(--transition);
            display: inline-flex;
            align-items: center;
            gap: 8px;
            text-align: center;
            justify-content: center;
        }
        .btn:hover {
            filter: brightness(90%);
            transform: translateY(-2px);
        }
        .btn:active {
            transform: translateY(0);
        }
        .btn-primary {
            background-color: var(--primary-color);
        }
        .btn-primary:hover {
            background-color: var(--primary-dark);
        }
        .btn-secondary {
            background-color: var(--secondary-color);
        }
        .btn-secondary:hover {
            background-color: var(--secondary-dark);
        }
        .btn-danger {
            background-color: var(--danger-color);
        }
        .btn-danger:hover {
            background-color: var(--danger-dark);
        }
        .btn-lg {
            padding: 15px 25px;
            font-size: 1.1rem;
        }
        .btn-block {
            display: block;
            width: 100%;
        }
        .main-menu {
            display: flex;
            gap: 12px;
            margin-bottom: 20px;
            flex-wrap: wrap;
            justify-content: center;
        }
        .card {
            background-color: var(--white);
            border-radius: var(--border-radius);
            box-shadow: var(--box-shadow);
            padding: 20px;
            margin-bottom: 20px;
            transition: var(--transition);
        }
        .card-title {
            color: var(--secondary-color);
            margin-top: 0;
            margin-bottom: 20px;
            font-size: 1.4rem;
            font-weight: 700;
            text-align: center;
            padding-bottom: 10px;
            border-bottom: 2px solid var(--light-color);
        }
        .form-group {
            margin-bottom: 20px;
        }
        .form-label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: var(--secondary-color);
            font-size: 1rem;
        }
        .form-control {
            width: 100%;
            padding: 12px 15px;
            border: 2px solid #ddd;
            border-radius: var(--border-radius);
            box-sizing: border-box;
            font-size: 1rem;
            transition: var(--transition);
            background-color: #f9f9f9;
        }
        .form-control:focus {
            border-color: var(--primary-color);
            outline: none;
            background-color: var(--white);
            box-shadow: 0 0 0 3px rgba(39, 174, 96, 0.2);
        }
        textarea.form-control {
            height: 120px;
            resize: vertical;
        }
        .camera-section {
            margin: 25px 0;
            text-align: center;
            border: 2px dashed #ddd;
            padding: 20px;
            border-radius: var(--border-radius);
            background-color: #f9f9f9;
        }
        .camera-title {
            margin-top: 0;
            margin-bottom: 15px;
            color: var(--secondary-color);
            font-size: 1.2rem;
        }
        #camera-preview {
            width: 100%;
            max-width: 100%;
            background-color: #eee;
            margin-bottom: 15px;
            border-radius: var(--border-radius);
            display: none;
        }
        #camera-preview.active {
            display: block;
        }
        .camera-options {
            display: flex;
            gap: 10px;
            justify-content: center;
            flex-wrap: wrap;
            margin-top: 15px;
        }
        .camera-option-btn {
            flex: 1;
            min-width: 150px;
        }
        #captured-images {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            margin-top: 20px;
            justify-content: center;
        }
        .image-container {
            position: relative;
            width: 150px;
            height: 150px;
            border-radius: var(--border-radius);
            overflow: hidden;
            box-shadow: var(--box-shadow);
        }
        .image-container img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }
        .delete-image {
            position: absolute;
            top: 8px;
            right: 8px;
            background-color: var(--danger-color);
            color: var(--white);
            border: none;
            border-radius: 50%;
            width: 30px;
            height: 30px;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            opacity: 0.9;
            transition: var(--transition);
        }
        .delete-image:hover {
            opacity: 1;
            transform: scale(1.1);
        }
        .records-table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
            box-shadow: 0 1px 3px rgba(0,0,0,0.1);
        }
        .records-table th, .records-table td {
            padding: 14px 16px;
            text-align: right;
            border-bottom: 1px solid #e0e0e0;
        }
        .records-table th {
            background-color: var(--secondary-color);
            color: var(--white);
            font-weight: 600;
            position: sticky;
            top: 0;
        }
        .records-table tr:hover {
            background-color: #f5f5f5;
        }
        .action-btn {
            padding: 10px 15px;
            border: none;
            border-radius: var(--border-radius);
            cursor: pointer;
            margin-left: 5px;
            display: inline-flex;
            align-items: center;
            gap: 5px;
            font-size: 0.9rem;
            transition: var(--transition);
            margin-bottom: 5px;
            width: 100%;
            justify-content: center;
        }
        .pagination {
            display: flex;
            justify-content: center;
            margin-top: 25px;
            gap: 8px;
            flex-wrap: wrap;
        }
        .page-btn {
            min-width: 40px;
        }
        .search-container {
            margin-bottom: 20px;
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
        }
        .search-input {
            flex: 1;
            min-width: 200px;
            padding: 12px 15px;
            border: 2px solid #ddd;
            border-radius: var(--border-radius);
            font-size: 1rem;
        }
        .no-records {
            text-align: center;
            padding: 30px;
            color: var(--gray);
            font-size: 1.1rem;
        }
        .record-details {
            margin-top: 20px;
        }
        .detail-row {
            display: flex;
            margin-bottom: 15px;
            flex-wrap: wrap;
        }
        .detail-label {
            font-weight: 600;
            width: 150px;
            color: var(--secondary-color);
            margin-bottom: 5px;
        }
        .detail-value {
            flex: 1;
            min-width: 200px;
            padding: 10px;
            background-color: #f9f9f9;
            border-radius: var(--border-radius);
        }
        .detail-images {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            margin-top: 25px;
            justify-content: center;
        }
        .detail-image {
            width: 100%;
            max-width: 300px;
            height: auto;
            object-fit: cover;
            border-radius: var(--border-radius);
            box-shadow: var(--box-shadow);
        }
        .back-btn {
            margin-bottom: 20px;
        }
        .hidden {
            display: none !important;
        }
        .file-input-container {
            position: relative;
            overflow: hidden;
            display: inline-block;
            width: 100%;
        }
        .file-input-container input[type="file"] {
            position: absolute;
            left: 0;
            top: 0;
            opacity: 0;
            width: 100%;
            height: 100%;
            cursor: pointer;
        }
        .action-buttons {
            display: flex;
            flex-direction: column;
            gap: 8px;
            margin-top: 10px;
        }
        @media (max-width: 768px) {
            .container {
                padding: 10px;
            }
            .header-content {
                flex-direction: column;
                text-align: center;
            }
            .lang-switcher {
                justify-content: center;
                margin-top: 10px;
            }
            .main-menu {
                gap: 8px;
            }
            .card {
                padding: 15px;
            }
            .records-table th, .records-table td {
                padding: 10px 12px;
                font-size: 0.9rem;
            }
            .action-btn {
                padding: 10px 12px;
                font-size: 0.9rem;
            }
            .detail-label {
                width: 100%;
            }
            .detail-value {
                width: 100%;
            }
            .btn {
                padding: 12px 18px;
            }
            .camera-option-btn {
                min-width: 100%;
            }
        }
        @media (max-width: 480px) {
            h1 {
                font-size: 1.3rem;
            }
            .card-title {
                font-size: 1.2rem;
            }
            .form-control {
                padding: 10px 12px;
            }
            .records-table {
                display: block;
                overflow-x: auto;
            }
            .image-container {
                width: 120px;
                height: 120px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <div class="header-content">
                <h1 lang="ar">نظام تسجيل الآفات والأمراض النباتية</h1>
                <h1 lang="en" class="hidden">Plant Pest & Disease Recording System</h1>
                <div class="lang-switcher">
                    <button class="btn btn-secondary" onclick="switchLanguage('ar')">
                        <i class="fas fa-language"></i>
                        <span lang="ar">العربية</span>
                        <span lang="en" class="hidden">Arabic</span>
                    </button>
                    <button class="btn btn-secondary" onclick="switchLanguage('en')">
                        <i class="fas fa-language"></i>
                        <span lang="ar">English</span>
                        <span lang="en" class="hidden">English</span>
                    </button>
                </div>
            </div>
        </header>
        <div class="main-menu">
            <button class="btn btn-primary btn-lg" onclick="showSection('record-section')" id="record-btn">
                <i class="fas fa-plus-circle"></i>
                <span lang="ar">تسجيل إصابة جديدة</span>
                <span lang="en" class="hidden">New Record</span>
            </button>
            <button class="btn btn-primary btn-lg" onclick="showSection('records-section')" id="records-btn">
                <i class="fas fa-list"></i>
                <span lang="ar">قائمة الإصابات</span>
                <span lang="en" class="hidden">Records List</span>
            </button>
        </div>
        
        <!-- تسجيل إصابة جديدة -->
        <div class="card" id="record-section">
            <h2 class="card-title" lang="ar">تسجيل إصابة جديدة</h2>
            <h2 class="card-title" lang="en" class="hidden">New Pest/Disease Record</h2>
            <form id="pestForm">
                <div class="form-group">
                    <label for="recorder-name" class="form-label" lang="ar">اسم المُسجل</label>
                    <label for="recorder-name" class="form-label" lang="en" class="hidden">Recorder Name</label>
                    <input type="text" id="recorder-name" class="form-control" required>
                </div>
                
                <div class="form-group">
                    <label for="discovery-date" class="form-label" lang="ar">تاريخ الاكتشاف</label>
                    <label for="discovery-date" class="form-label" lang="en" class="hidden">Discovery Date</label>
                    <input type="date" id="discovery-date" class="form-control" required>
                </div>
                
                <div class="form-row">
                    <div class="form-group" style="flex: 1;">
                        <label for="pest-name" class="form-label" lang="ar">اسم الإصابة المحتملة</label>
                        <label for="pest-name" class="form-label" lang="en" class="hidden">Potential Pest/Disease Name</label>
                        <input type="text" id="pest-name" class="form-control" required>
                    </div>
                    <div class="form-group" style="flex: 1;">
                        <label for="scientific-name" class="form-label" lang="ar">الاسم العلمي</label>
                        <label for="scientific-name" class="form-label" lang="en" class="hidden">Scientific Name</label>
                        <input type="text" id="scientific-name" class="form-control">
                    </div>
                </div>
                
                <div class="form-group">
                    <label for="affected-crop" class="form-label" lang="ar">المحصول المصاب</label>
                    <label for="affected-crop" class="form-label" lang="en" class="hidden">Affected Crop</label>
                    <input type="text" id="affected-crop" class="form-control" required>
                </div>
                
                <div class="form-group">
                    <label for="symptoms" class="form-label" lang="ar">أعراض الإصابة</label>
                    <label for="symptoms" class="form-label" lang="en" class="hidden">Symptoms</label>
                    <textarea id="symptoms" class="form-control" required></textarea>
                </div>
                
                <div class="camera-section">
                    <h3 class="camera-title" lang="ar">تصوير الإصابة</h3>
                    <h3 class="camera-title" lang="en" class="hidden">Capture Images</h3>
                    
                    <div class="camera-options">
                        <div class="file-input-container">
                            <button type="button" class="btn btn-primary camera-option-btn">
                                <i class="fas fa-upload"></i>
                                <span lang="ar">رفع صورة من الجهاز</span>
                                <span lang="en" class="hidden">Upload Image</span>
                            </button>
                            <input type="file" id="file-input" accept="image/*" onchange="handleFileUpload(this.files)">
                        </div>
                        
                        <button type="button" class="btn btn-primary camera-option-btn" onclick="openCamera()">
                            <i class="fas fa-camera"></i>
                            <span lang="ar">التقاط صورة من الكاميرا</span>
                            <span lang="en" class="hidden">Take Photo</span>
                        </button>
                    </div>
                    
                    <div id="captured-images"></div>
                </div>
                
                <div class="form-group">
                    <label for="pesticide" class="form-label" lang="ar">المكافحة الكيميائية (اسم المبيد)</label>
                    <label for="pesticide" class="form-label" lang="en" class="hidden">Chemical Control (Pesticide Name)</label>
                    <input type="text" id="pesticide" class="form-control">
                </div>
                
                <div class="form-group">
                    <label for="notes" class="form-label" lang="ar">ملاحظات إضافية</label>
                    <label for="notes" class="form-label" lang="en" class="hidden">Additional Notes</label>
                    <textarea id="notes" class="form-control"></textarea>
                </div>
                
                <button type="submit" class="btn btn-primary btn-lg btn-block">
                    <i class="fas fa-save"></i>
                    <span lang="ar">حفظ البيانات</span>
                    <span lang="en" class="hidden">Save Record</span>
                </button>
            </form>
        </div>
        
        <!-- قائمة الإصابات -->
        <div class="card hidden" id="records-section">
            <h2 class="card-title" lang="ar">قائمة الإصابات</h2>
            <h2 class="card-title" lang="en" class="hidden">Records List</h2>
            
            <div class="search-container">
                <input type="text" class="search-input" id="search-input" placeholder="ابحث باسم الإصابة أو المحصول..." lang="ar">
                <input type="text" class="search-input hidden" id="search-input-en" placeholder="Search by pest or crop..." lang="en">
                <button class="btn btn-primary" onclick="searchRecords()">
                    <i class="fas fa-search"></i>
                    <span lang="ar">بحث</span>
                    <span lang="en" class="hidden">Search</span>
                </button>
            </div>
            
            <div class="table-responsive">
                <table class="records-table">
                    <thead>
                        <tr>
                            <th lang="ar">التاريخ</th>
                            <th lang="en" class="hidden">Date</th>
                            <th lang="ar">اسم الإصابة</th>
                            <th lang="en" class="hidden">Pest/Disease</th>
                            <th lang="ar">المحصول</th>
                            <th lang="en" class="hidden">Crop</th>
                            <th lang="ar">المُسجل</th>
                            <th lang="en" class="hidden">Recorder</th>
                            <th lang="ar">الإجراءات</th>
                            <th lang="en" class="hidden">Actions</th>
                        </tr>
                    </thead>
                    <tbody id="records-table-body">
                        <!-- سيتم ملؤها بالبيانات من localStorage -->
                    </tbody>
                </table>
            </div>
            
            <div class="no-records hidden" id="no-records">
                <i class="fas fa-info-circle" style="font-size: 2rem; margin-bottom: 10px;"></i>
                <p lang="ar">لا توجد سجلات مسجلة</p>
                <p lang="en" class="hidden">No records found</p>
            </div>
            
            <div class="pagination" id="pagination">
                <!-- سيتم ملؤها بالترقيم -->
            </div>
        </div>
        
        <!-- تفاصيل الإصابة -->
        <div class="card hidden" id="record-details-section">
            <button class="btn btn-secondary back-btn" onclick="showSection('records-section')">
                <i class="fas fa-arrow-left"></i>
                <span lang="ar">العودة للقائمة</span>
                <span lang="en" class="hidden">Back to List</span>
            </button>
            
            <h2 class="card-title" id="detail-title" lang="ar">تفاصيل الإصابة</h2>
            <h2 class="card-title" id="detail-title-en" lang="en" class="hidden">Record Details</h2>
            
            <div class="record-details" id="record-details">
                <!-- سيتم ملؤها بالتفاصيل -->
            </div>
            
            <div class="action-buttons" id="record-actions">
                <!-- سيتم ملؤها بأزرار الإجراءات -->
            </div>
        </div>
    </div>

    <script>
        // المتغيرات العامة
        let currentLanguage = 'ar';
        let records = JSON.parse(localStorage.getItem('pestRecords')) || [];
        let currentPage = 1;
        const recordsPerPage = 5;
        let stream = null;
        let currentRecordId = null;
        
        // تهيئة الصفحة عند التحميل
        document.addEventListener('DOMContentLoaded', function() {
            // تعيين تاريخ اليوم كتاريخ افتراضي
            const today = new Date().toISOString().split('T')[0];
            document.getElementById('discovery-date').value = today;
            
            // عرض قسم تسجيل الإصابة الجديدة افتراضيًا
            showSection('record-section');
            
            // تحميل السجلات إذا وجدت
            if (records.length > 0) {
                renderRecordsTable();
            } else {
                document.getElementById('no-records').classList.remove('hidden');
            }
            
            // تهيئة مكتبة jsPDF
            window.jsPDF = window.jspdf.jsPDF;
        });
        
        // تبديل اللغة
        function switchLanguage(lang) {
            currentLanguage = lang;
            // إخفاء جميع عناصر اللغة
            document.querySelectorAll('[lang]').forEach(el => {
                if (el.tagName !== 'HTML') {
                    el.classList.add('hidden');
                }
            });
            // إظهار العناصر للغة المحددة
            document.querySelectorAll(`[lang="${lang}"]`).forEach(el => {
                el.classList.remove('hidden');
            });
            // تعيين اتجاه الصفحة
            document.documentElement.lang = lang;
            document.documentElement.dir = lang === 'ar' ? 'rtl' : 'ltr';
            // تحديث جدول السجلات عند تغيير اللغة
            if (!document.getElementById('records-section').classList.contains('hidden')) {
                renderRecordsTable();
            }
            // تحديث تفاصيل السجل إذا كان معروضًا
            if (!document.getElementById('record-details-section').classList.contains('hidden') && currentRecordId) {
                viewRecordDetails(currentRecordId);
            }
        }
        
        // عرض قسم معين وإخفاء الأقسام الأخرى
        function showSection(sectionId) {
            // إيقاف الكاميرا إذا كانت تعمل
            if (stream && sectionId !== 'record-section') {
                stopCamera();
            }
            
            // إخفاء جميع الأقسام
            document.querySelectorAll('.card').forEach(section => {
                section.classList.add('hidden');
            });
            
            // إظهار القسم المطلوب
            document.getElementById(sectionId).classList.remove('hidden');
            
            // إذا كان القسم هو قائمة السجلات، نقوم بتحديث الجدول
            if (sectionId === 'records-section') {
                renderRecordsTable();
            }
            
            // إذا كان القسم هو تسجيل جديد، نعيد تعيين النموذج
            if (sectionId === 'record-section') {
                document.getElementById('pestForm').reset();
                document.getElementById('captured-images').innerHTML = '';
                document.getElementById('discovery-date').value = new Date().toISOString().split('T')[0];
            }
        }
        
        // فتح الكاميرا لالتقاط صورة
        function openCamera() {
            // إيقاف الكاميرا إذا كانت تعمل بالفعل
            if (stream) {
                stopCamera();
            }
            
            const constraints = {
                video: {
                    facingMode: "environment", // استخدام الكاميرا الخلفية
                    width: { ideal: 1280 },
                    height: { ideal: 720 }
                },
                audio: false
            };
            
            navigator.mediaDevices.getUserMedia(constraints)
                .then(function(mediaStream) {
                    stream = mediaStream;
                    const video = document.createElement('video');
                    video.srcObject = stream;
                    video.play();
                    
                    // إنشاء نافذة للعرض والتقاط الصورة
                    const cameraWindow = window.open('', 'Camera', 'width=800,height=600');
                    cameraWindow.document.body.style.textAlign = 'center';
                    cameraWindow.document.body.style.padding = '20px';
                    
                    // إضافة عنصر الفيديو
                    cameraWindow.document.body.appendChild(video);
                    video.style.maxWidth = '100%';
                    video.style.borderRadius = '10px';
                    video.style.marginBottom = '20px';
                    
                    // زر التقاط الصورة
                    const captureBtn = cameraWindow.document.createElement('button');
                    captureBtn.textContent = currentLanguage === 'ar' ? 'التقاط صورة' : 'Capture Photo';
                    captureBtn.style.padding = '12px 24px';
                    captureBtn.style.backgroundColor = '#27ae60';
                    captureBtn.style.color = 'white';
                    captureBtn.style.border = 'none';
                    captureBtn.style.borderRadius = '5px';
                    captureBtn.style.cursor = 'pointer';
                    captureBtn.style.fontSize = '16px';
                    captureBtn.onclick = function() {
                        const canvas = document.createElement('canvas');
                        canvas.width = video.videoWidth;
                        canvas.height = video.videoHeight;
                        const ctx = canvas.getContext('2d');
                        ctx.drawImage(video, 0, 0, canvas.width, canvas.height);
                        
                        const imgData = canvas.toDataURL('image/jpeg');
                        addCapturedImage(imgData);
                        
                        // إغلاق النافذة وإيقاف الكاميرا
                        cameraWindow.close();
                        stopCamera();
                        
                        showToast(currentLanguage === 'ar' ? 'تم التقاط الصورة بنجاح' : 'Photo captured successfully');
                    };
                    
                    cameraWindow.document.body.appendChild(captureBtn);
                    
                    // زر الإغلاق
                    const closeBtn = cameraWindow.document.createElement('button');
                    closeBtn.textContent = currentLanguage === 'ar' ? 'إغلاق' : 'Close';
                    closeBtn.style.padding = '12px 24px';
                    closeBtn.style.backgroundColor = '#e74c3c';
                    closeBtn.style.color = 'white';
                    closeBtn.style.border = 'none';
                    closeBtn.style.borderRadius = '5px';
                    closeBtn.style.cursor = 'pointer';
                    closeBtn.style.fontSize = '16px';
                    closeBtn.style.marginLeft = '10px';
                    closeBtn.onclick = function() {
                        cameraWindow.close();
                        stopCamera();
                    };
                    
                    cameraWindow.document.body.appendChild(closeBtn);
                })
                .catch(function(err) {
                    console.error("Error accessing camera:", err);
                    alert(currentLanguage === 'ar' ? 
                        "تعذر الوصول إلى الكاميرا. يرجى التحقق من الأذونات." : 
                        "Could not access camera. Please check permissions.");
                });
        }
        
        // إيقاف الكاميرا
        function stopCamera() {
            if (stream) {
                stream.getTracks().forEach(track => track.stop());
                stream = null;
            }
        }
        
        // معالجة رفع الصور من الجهاز
        function handleFileUpload(files) {
            if (files && files.length > 0) {
                const file = files[0];
                if (file.type.match('image.*')) {
                    const reader = new FileReader();
                    reader.onload = function(e) {
                        addCapturedImage(e.target.result);
                        showToast(currentLanguage === 'ar' ? 'تم رفع الصورة بنجاح' : 'Image uploaded successfully');
                    };
                    reader.readAsDataURL(file);
                } else {
                    alert(currentLanguage === 'ar' ? 'الملف المحدد ليس صورة' : 'The selected file is not an image');
                }
            }
        }
        
        // إظهار رسالة toast
        function showToast(message) {
            const toast = document.createElement('div');
            toast.style.position = 'fixed';
            toast.style.bottom = '20px';
            toast.style.left = '50%';
            toast.style.transform = 'translateX(-50%)';
            toast.style.backgroundColor = 'rgba(0,0,0,0.7)';
            toast.style.color = 'white';
            toast.style.padding = '10px 20px';
            toast.style.borderRadius = '20px';
            toast.style.zIndex = '1000';
            toast.style.transition = 'all 0.3s ease';
            toast.textContent = message;
            document.body.appendChild(toast);
            
            setTimeout(() => {
                toast.style.opacity = '0';
                setTimeout(() => toast.remove(), 300);
            }, 3000);
        }
        
        // إضافة الصورة الملتقطة إلى القسم
        function addCapturedImage(imgData) {
            const container = document.createElement('div');
            container.className = 'image-container';
            
            const img = document.createElement('img');
            img.src = imgData;
            
            const deleteBtn = document.createElement('button');
            deleteBtn.className = 'delete-image';
            deleteBtn.innerHTML = '<i class="fas fa-times"></i>';
            deleteBtn.onclick = function() {
                container.remove();
            };
            
            container.appendChild(img);
            container.appendChild(deleteBtn);
            document.getElementById('captured-images').appendChild(container);
        }
        
        // حفظ السجل الجديد
        document.getElementById('pestForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            // جمع بيانات النموذج
            const formData = {
                id: Date.now().toString(),
                recorderName: document.getElementById('recorder-name').value,
                date: document.getElementById('discovery-date').value,
                pestName: document.getElementById('pest-name').value,
                scientificName: document.getElementById('scientific-name').value,
                affectedCrop: document.getElementById('affected-crop').value,
                symptoms: document.getElementById('symptoms').value,
                pesticide: document.getElementById('pesticide').value,
                notes: document.getElementById('notes').value,
                images: Array.from(document.querySelectorAll('#captured-images .image-container img')).map(img => img.src),
                createdAt: new Date().toISOString()
            };
            
            // إضافة السجل إلى القائمة
            records.unshift(formData);
            localStorage.setItem('pestRecords', JSON.stringify(records));
            
            // إظهار رسالة نجاح
            showToast(currentLanguage === 'ar' ? 'تم حفظ السجل بنجاح!' : 'Record saved successfully!');
            
            // إعادة تعيين النموذج
            this.reset();
            document.getElementById('captured-images').innerHTML = '';
            document.getElementById('discovery-date').value = new Date().toISOString().split('T')[0];
            
            // إيقاف الكاميرا إذا كانت تعمل
            if (stream) {
                stopCamera();
            }
            
            // التبديل إلى قائمة السجلات
            showSection('records-section');
        });
        
        // عرض السجلات في الجدول
        function renderRecordsTable(page = 1) {
            currentPage = page;
            const startIndex = (page - 1) * recordsPerPage;
            const endIndex = startIndex + recordsPerPage;
            const paginatedRecords = records.slice(startIndex, endIndex);
            const tableBody = document.getElementById('records-table-body');
            tableBody.innerHTML = '';
            
            if (paginatedRecords.length === 0) {
                document.getElementById('no-records').classList.remove('hidden');
                document.getElementById('pagination').innerHTML = '';
                return;
            } else {
                document.getElementById('no-records').classList.add('hidden');
            }
            
            paginatedRecords.forEach(record => {
                const row = document.createElement('tr');
                
                // التاريخ
                const dateCell = document.createElement('td');
                dateCell.textContent = record.date;
                row.appendChild(dateCell);
                
                // اسم الإصابة
                const nameCell = document.createElement('td');
                nameCell.textContent = record.pestName;
                row.appendChild(nameCell);
                
                // المحصول
                const cropCell = document.createElement('td');
                cropCell.textContent = record.affectedCrop;
                row.appendChild(cropCell);
                
                // اسم المُسجل
                const recorderCell = document.createElement('td');
                recorderCell.textContent = record.recorderName || '-';
                row.appendChild(recorderCell);
                
                // الإجراءات
                const actionsCell = document.createElement('td');
                
                // زر لعرض الإجراءات
                const actionsBtn = document.createElement('button');
                actionsBtn.className = 'btn btn-primary';
                actionsBtn.innerHTML = '<i class="fas fa-ellipsis-h"></i>';
                actionsBtn.onclick = () => showRecordActions(record.id);
                actionsCell.appendChild(actionsBtn);
                
                row.appendChild(actionsCell);
                tableBody.appendChild(row);
            });
            
            // إنشاء الترقيم
            renderPagination();
        }
        
        // عرض إجراءات السجل
        function showRecordActions(recordId) {
            const record = records.find(r => r.id === recordId);
            if (!record) return;
            
            currentRecordId = recordId;
            viewRecordDetails(recordId);
        }
        
        // إنشاء الترقيم
        function renderPagination() {
            const totalPages = Math.ceil(records.length / recordsPerPage);
            const paginationDiv = document.getElementById('pagination');
            paginationDiv.innerHTML = '';
            
            if (totalPages <= 1) return;
            
            // زر الصفحة السابقة
            if (currentPage > 1) {
                const prevBtn = document.createElement('button');
                prevBtn.className = 'btn btn-secondary page-btn';
                prevBtn.innerHTML = '<i class="fas fa-chevron-right"></i>';
                prevBtn.onclick = () => renderRecordsTable(currentPage - 1);
                paginationDiv.appendChild(prevBtn);
            }
            
            // أزرار الصفحات
            for (let i = 1; i <= totalPages; i++) {
                const pageBtn = document.createElement('button');
                pageBtn.className = 'btn btn-secondary page-btn' + (i === currentPage ? ' active' : '');
                pageBtn.textContent = i;
                pageBtn.onclick = () => renderRecordsTable(i);
                paginationDiv.appendChild(pageBtn);
            }
            
            // زر الصفحة التالية
            if (currentPage < totalPages) {
                const nextBtn = document.createElement('button');
                nextBtn.className = 'btn btn-secondary page-btn';
                nextBtn.innerHTML = '<i class="fas fa-chevron-left"></i>';
                nextBtn.onclick = () => renderRecordsTable(currentPage + 1);
                paginationDiv.appendChild(nextBtn);
            }
        }
        
        // عرض تفاصيل السجل
        function viewRecordDetails(recordId) {
            const record = records.find(r => r.id === recordId);
            if (!record) return;
            
            currentRecordId = recordId;
            const detailsDiv = document.getElementById('record-details');
            detailsDiv.innerHTML = `
                <div class="detail-row">
                    <div class="detail-label" lang="ar">اسم المُسجل:</div>
                    <div class="detail-label" lang="en" class="hidden">Recorder Name:</div>
                    <div class="detail-value">${record.recorderName || '-'}</div>
                </div>
                <div class="detail-row">
                    <div class="detail-label" lang="ar">تاريخ الاكتشاف:</div>
                    <div class="detail-label" lang="en" class="hidden">Discovery Date:</div>
                    <div class="detail-value">${record.date}</div>
                </div>
                <div class="detail-row">
                    <div class="detail-label" lang="ar">اسم الإصابة:</div>
                    <div class="detail-label" lang="en" class="hidden">Pest/Disease Name:</div>
                    <div class="detail-value">${record.pestName}</div>
                </div>
                <div class="detail-row">
                    <div class="detail-label" lang="ar">الاسم العلمي:</div>
                    <div class="detail-label" lang="en" class="hidden">Scientific Name:</div>
                    <div class="detail-value">${record.scientificName || '-'}</div>
                </div>
                <div class="detail-row">
                    <div class="detail-label" lang="ar">المحصول المصاب:</div>
                    <div class="detail-label" lang="en" class="hidden">Affected Crop:</div>
                    <div class="detail-value">${record.affectedCrop}</div>
                </div>
                <div class="detail-row">
                    <div class="detail-label" lang="ar">أعراض الإصابة:</div>
                    <div class="detail-label" lang="en" class="hidden">Symptoms:</div>
                    <div class="detail-value">${record.symptoms}</div>
                </div>
                <div class="detail-row">
                    <div class="detail-label" lang="ar">المكافحة الكيميائية:</div>
                    <div class="detail-label" lang="en" class="hidden">Chemical Control:</div>
                    <div class="detail-value">${record.pesticide || '-'}</div>
                </div>
                <div class="detail-row">
                    <div class="detail-label" lang="ar">ملاحظات إضافية:</div>
                    <div class="detail-label" lang="en" class="hidden">Additional Notes:</div>
                    <div class="detail-value">${record.notes || '-'}</div>
                </div>
                
                ${record.images && record.images.length > 0 ? `
                <h3 style="margin-top: 25px; color: var(--secondary-color);" lang="ar">صور الإصابة:</h3>
                <h3 style="margin-top: 25px; color: var(--secondary-color);" lang="en" class="hidden">Pest/Disease Images:</h3>
                <div class="detail-images">
                    ${record.images.map(img => `<img src="${img}" class="detail-image">`).join('')}
                </div>
                ` : ''}
            `;
            
            // إضافة أزرار الإجراءات
            const actionsDiv = document.getElementById('record-actions');
            actionsDiv.innerHTML = '';
            
            // زر العودة
            const backBtn = document.createElement('button');
            backBtn.className = 'btn btn-secondary';
            backBtn.innerHTML = '<i class="fas fa-arrow-left"></i> <span lang="ar">العودة</span><span lang="en" class="hidden">Back</span>';
            backBtn.onclick = () => showSection('records-section');
            actionsDiv.appendChild(backBtn);
            
            // زر التعديل
            const editBtn = document.createElement('button');
            editBtn.className = 'btn btn-primary';
            editBtn.innerHTML = '<i class="fas fa-edit"></i> <span lang="ar">تعديل</span><span lang="en" class="hidden">Edit</span>';
            editBtn.onclick = () => editRecord(record.id);
            actionsDiv.appendChild(editBtn);
            
            // زر الحذف
            const deleteBtn = document.createElement('button');
            deleteBtn.className = 'btn btn-danger';
            deleteBtn.innerHTML = '<i class="fas fa-trash"></i> <span lang="ar">حذف</span><span lang="en" class="hidden">Delete</span>';
            deleteBtn.onclick = () => deleteRecord(record.id);
            actionsDiv.appendChild(deleteBtn);
            
            // زر PDF
            const pdfBtn = document.createElement('button');
            pdfBtn.className = 'btn btn-secondary';
            pdfBtn.innerHTML = '<i class="fas fa-file-pdf"></i> <span lang="ar">تحميل PDF</span><span lang="en" class="hidden">Download PDF</span>';
            pdfBtn.onclick = () => generatePDF(record.id);
            actionsDiv.appendChild(pdfBtn);
            
            showSection('record-details-section');
        }
        
        // تعديل السجل
        function editRecord(recordId) {
            const record = records.find(r => r.id === recordId);
            if (!record) return;
            
            // ملء النموذج ببيانات السجل
            document.getElementById('recorder-name').value = record.recorderName || '';
            document.getElementById('discovery-date').value = record.date;
            document.getElementById('pest-name').value = record.pestName;
            document.getElementById('scientific-name').value = record.scientificName || '';
            document.getElementById('affected-crop').value = record.affectedCrop;
            document.getElementById('symptoms').value = record.symptoms;
            document.getElementById('pesticide').value = record.pesticide || '';
            document.getElementById('notes').value = record.notes || '';
            
            // عرض الصور إذا وجدت
            const imagesContainer = document.getElementById('captured-images');
            imagesContainer.innerHTML = '';
            if (record.images && record.images.length > 0) {
                record.images.forEach(imgData => {
                    addCapturedImage(imgData);
                });
            }
            
            // حذف السجل القديم
            records = records.filter(r => r.id !== recordId);
            localStorage.setItem('pestRecords', JSON.stringify(records));
            
            // التبديل إلى قسم التسجيل
            showSection('record-section');
            
            // إظهار رسالة
            showToast(currentLanguage === 'ar' ? 'يمكنك الآن تعديل السجل' : 'You can now edit the record');
        }
        
        // حذف السجل
        function deleteRecord(recordId) {
            if (confirm(currentLanguage === 'ar' ? 'هل أنت متأكد من حذف هذا السجل؟' : 'Are you sure you want to delete this record?')) {
                records = records.filter(r => r.id !== recordId);
                localStorage.setItem('pestRecords', JSON.stringify(records));
                renderRecordsTable(currentPage);
                
                if (records.length === 0) {
                    document.getElementById('no-records').classList.remove('hidden');
                }
                
                showToast(currentLanguage === 'ar' ? 'تم حذف السجل بنجاح' : 'Record deleted successfully');
                
                // العودة إلى قائمة السجلات
                showSection('records-section');
            }
        }
        
        // البحث في السجلات
        function searchRecords() {
            const searchTerm = currentLanguage === 'ar' ? 
                document.getElementById('search-input').value.toLowerCase() : 
                document.getElementById('search-input-en').value.toLowerCase();
                
            if (!searchTerm) {
                renderRecordsTable();
                return;
            }
            
            const filteredRecords = records.filter(record => 
                (record.recorderName && record.recorderName.toLowerCase().includes(searchTerm)) ||
                record.pestName.toLowerCase().includes(searchTerm) ||
                (record.scientificName && record.scientificName.toLowerCase().includes(searchTerm)) ||
                record.affectedCrop.toLowerCase().includes(searchTerm) ||
                record.symptoms.toLowerCase().includes(searchTerm) ||
                (record.pesticide && record.pesticide.toLowerCase().includes(searchTerm)) ||
                (record.notes && record.notes.toLowerCase().includes(searchTerm))
            );
            
            renderSearchResults(filteredRecords);
        }
        
        // عرض نتائج البحث
        function renderSearchResults(filteredRecords) {
            const tableBody = document.getElementById('records-table-body');
            tableBody.innerHTML = '';
            
            if (filteredRecords.length === 0) {
                document.getElementById('no-records').classList.remove('hidden');
                document.getElementById('pagination').innerHTML = '';
                return;
            } else {
                document.getElementById('no-records').classList.add('hidden');
            }
            
            filteredRecords.forEach(record => {
                const row = document.createElement('tr');
                
                // التاريخ
                const dateCell = document.createElement('td');
                dateCell.textContent = record.date;
                row.appendChild(dateCell);
                
                // اسم الإصابة
                const nameCell = document.createElement('td');
                nameCell.textContent = record.pestName;
                row.appendChild(nameCell);
                
                // المحصول
                const cropCell = document.createElement('td');
                cropCell.textContent = record.affectedCrop;
                row.appendChild(cropCell);
                
                // اسم المُسجل
                const recorderCell = document.createElement('td');
                recorderCell.textContent = record.recorderName || '-';
                row.appendChild(recorderCell);
                
                // الإجراءات
                const actionsCell = document.createElement('td');
                
                // زر لعرض الإجراءات
                const actionsBtn = document.createElement('button');
                actionsBtn.className = 'btn btn-primary';
                actionsBtn.innerHTML = '<i class="fas fa-ellipsis-h"></i>';
                actionsBtn.onclick = () => showRecordActions(record.id);
                actionsCell.appendChild(actionsBtn);
                
                row.appendChild(actionsCell);
                tableBody.appendChild(row);
            });
            
            document.getElementById('pagination').innerHTML = '';
        }
        
        // توليد ملف PDF مع دعم اللغة العربية
        async function generatePDF(recordId) {
            const record = records.find(r => r.id === recordId);
            if (!record) return;
            
            // إظهار رسالة تحميل
            const loadingToast = document.createElement('div');
            loadingToast.style.position = 'fixed';
            loadingToast.style.top = '50%';
            loadingToast.style.left = '50%';
            loadingToast.style.transform = 'translate(-50%, -50%)';
            loadingToast.style.backgroundColor = 'rgba(0,0,0,0.8)';
            loadingToast.style.color = 'white';
            loadingToast.style.padding = '15px 25px';
            loadingToast.style.borderRadius = '5px';
            loadingToast.style.zIndex = '1000';
            loadingToast.style.display = 'flex';
            loadingToast.style.alignItems = 'center';
            loadingToast.style.gap = '10px';
            loadingToast.innerHTML = `<i class="fas fa-spinner fa-spin"></i> <span lang="ar">جاري إنشاء PDF...</span><span lang="en" class="hidden">Generating PDF...</span>`;
            document.body.appendChild(loadingToast);
            
            try {
                // إنشاء PDF جديد
                const { jsPDF } = window.jspdf;
                const pdf = new jsPDF({
                    orientation: 'portrait',
                    unit: 'mm',
                    format: 'a4'
                });
                
                // إضافة خط Amiri للغة العربية
                pdf.addFont('https://fonts.gstatic.com/s/amiri/v24/J7aRnpd8CGxBHpUrtLMA7w.woff2', 'Amiri', 'normal');
                pdf.setFont('Amiri');
                
                // إضافة عنوان التقرير
                pdf.setFontSize(18);
                pdf.setTextColor(44, 62, 80);
                pdf.setFont('Amiri', 'bold');
                
                // تحديد اتجاه النص بناءً على اللغة
                const title = currentLanguage === 'ar' ? 'تقرير الإصابة النباتية' : 'Plant Pest/Disease Report';
                const titleX = currentLanguage === 'ar' ? 180 : 105; // تعديل الموضع للغة العربية
                pdf.text(title, titleX, 20, { align: currentLanguage === 'ar' ? 'right' : 'center' });
                
                pdf.setFontSize(12);
                pdf.setTextColor(85, 85, 85);
                pdf.setFont('Amiri', 'normal');
                const reportDate = currentLanguage === 'ar' ? 
                    `تاريخ التقرير: ${new Date().toLocaleDateString('ar-EG')}` : 
                    `Report Date: ${new Date().toLocaleDateString('en-US')}`;
                pdf.text(reportDate, titleX, 30, { align: currentLanguage === 'ar' ? 'right' : 'center' });
                
                // إضافة معلومات الإصابة
                pdf.setFontSize(14);
                pdf.setTextColor(44, 62, 80);
                pdf.setFont('Amiri', 'bold');
                const infoTitle = currentLanguage === 'ar' ? 'معلومات الإصابة' : 'Pest/Disease Information';
                pdf.text(infoTitle, currentLanguage === 'ar' ? 180 : 15, 45, { align: currentLanguage === 'ar' ? 'right' : 'left' });
                
                pdf.setFontSize(12);
                pdf.setTextColor(0, 0, 0);
                pdf.setFont('Amiri', 'normal');
                
                let yPosition = 55;
                
                // معلومات النص الأساسية
                const recordInfo = [
                    { 
                        label: currentLanguage === 'ar' ? 'اسم المُسجل:' : 'Recorder Name:', 
                        value: record.recorderName || '-' 
                    },
                    { 
                        label: currentLanguage === 'ar' ? 'تاريخ الاكتشاف:' : 'Discovery Date:', 
                        value: record.date 
                    },
                    { 
                        label: currentLanguage === 'ar' ? 'اسم الإصابة:' : 'Pest/Disease Name:', 
                        value: record.pestName 
                    },
                    { 
                        label: currentLanguage === 'ar' ? 'الاسم العلمي:' : 'Scientific Name:', 
                        value: record.scientificName || '-' 
                    },
                    { 
                        label: currentLanguage === 'ar' ? 'المحصول المصاب:' : 'Affected Crop:', 
                        value: record.affectedCrop 
                    },
                    { 
                        label: currentLanguage === 'ar' ? 'أعراض الإصابة:' : 'Symptoms:', 
                        value: record.symptoms 
                    },
                    { 
                        label: currentLanguage === 'ar' ? 'المكافحة الكيميائية:' : 'Chemical Control:', 
                        value: record.pesticide || '-' 
                    },
                    { 
                        label: currentLanguage === 'ar' ? 'ملاحظات إضافية:' : 'Additional Notes:', 
                        value: record.notes || '-' 
                    }
                ];
                
                // إضافة المعلومات إلى PDF
                recordInfo.forEach(info => {
                    const text = `${info.label} ${info.value}`;
                    const textX = currentLanguage === 'ar' ? 180 : 15;
                    
                    // تقسيم النص الطويل إلى أسطر
                    const lines = pdf.splitTextToSize(text, 160);
                    
                    lines.forEach(line => {
                        pdf.text(line, textX, yPosition, { align: currentLanguage === 'ar' ? 'right' : 'left' });
                        yPosition += 7;
                    });
                });
                
                // إضافة الصور إذا وجدت
                if (record.images && record.images.length > 0) {
                    yPosition += 10;
                    pdf.setFontSize(14);
                    pdf.setTextColor(44, 62, 80);
                    pdf.setFont('Amiri', 'bold');
                    const imagesTitle = currentLanguage === 'ar' ? 'صور الإصابة' : 'Pest/Disease Images';
                    pdf.text(imagesTitle, currentLanguage === 'ar' ? 180 : 15, yPosition, { align: currentLanguage === 'ar' ? 'right' : 'left' });
                    yPosition += 10;
                    
                    // تحديد أبعاد الصور
                    const imgWidth = 80;
                    const imgHeight = 60;
                    let xPosition = currentLanguage === 'ar' ? 110 : 15;
                    
                    for (let i = 0; i < record.images.length; i++) {
                        if (i > 0 && i % 2 === 0) {
                            xPosition = currentLanguage === 'ar' ? 110 : 15;
                            yPosition += imgHeight + 10;
                            
                            // التحقق من وجود مساحة كافية في الصفحة
                            if (yPosition + imgHeight > 270) {
                                pdf.addPage();
                                yPosition = 20;
                                xPosition = currentLanguage === 'ar' ? 110 : 15;
                            }
                        }
                        
                        try {
                            // إضافة الصورة إلى PDF
                            pdf.addImage(record.images[i], 'JPEG', xPosition, yPosition, imgWidth, imgHeight);
                            xPosition += currentLanguage === 'ar' ? - (imgWidth + 10) : (imgWidth + 10);
                        } catch (error) {
                            console.error('Error adding image to PDF:', error);
                        }
                    }
                }
                
                // إضافة تذييل الصفحة
                pdf.setFontSize(10);
                pdf.setTextColor(119, 119, 119);
                pdf.setFont('Amiri', 'italic');
                const footerText = currentLanguage === 'ar' ? 
                    'تم إنشاء هذا التقرير باستخدام نظام تسجيل الآفات والأمراض النباتية' : 
                    'This report was generated using Plant Pest & Disease Recording System';
                pdf.text(footerText, 105, 287, { align: 'center' });
                
                // حفظ الملف
                pdf.save(`${record.pestName}_${record.date}.pdf`);
                
            } catch (error) {
                console.error('حدث خطأ أثناء إنشاء PDF:', error);
                alert(currentLanguage === 'ar' ? 
                    'حدث خطأ أثناء إنشاء الملف. يرجى المحاولة مرة أخرى.' : 
                    'Error generating PDF. Please try again.');
            } finally {
                // إخفاء رسالة التحميل
                loadingToast.remove();
            }
        }
    </script>
</body>
</html>
