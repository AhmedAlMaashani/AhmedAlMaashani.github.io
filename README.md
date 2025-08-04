<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>نظام تسجيل الآفات والأمراض النباتية</title>
    <!-- خط عربي عالي الجودة -->
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700&display=swap" rel="stylesheet">
    <!-- أيقونات فونت أوسوم -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- مكتبات PDF -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
    <style>
        :root {
            --primary: #27ae60;
            --secondary: #2c3e50;
            --danger: #e74c3c;
            --light: #f8f9fa;
            --dark: #333;
            --white: #fff;
            --border-radius: 12px;
            --shadow: 0 4px 20px rgba(0,0,0,0.1);
            --transition: all 0.3s ease;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            font-family: 'Cairo', 'Segoe UI', Tahoma, sans-serif;
            background-color: var(--light);
            color: var(--dark);
            line-height: 1.8;
            direction: rtl;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 15px;
            min-height: 100vh;
        }

        header {
            background: linear-gradient(135deg, var(--secondary), #1a2530);
            color: var(--white);
            padding: 18px 0;
            border-radius: var(--border-radius) var(--border-radius) 0 0;
            margin-bottom: 20px;
            box-shadow: var(--shadow);
        }

        .header-content {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 0 20px;
            flex-wrap: wrap;
            gap: 10px;
        }

        h1 {
            font-size: 1.5rem;
            font-weight: 700;
            text-shadow: 1px 1px 3px rgba(0,0,0,0.3);
        }

        .lang-switcher {
            display: flex;
            gap: 10px;
        }

        .lang-btn {
            padding: 10px 18px;
            background-color: var(--primary);
            color: var(--white);
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-weight: 600;
            font-size: 0.95rem;
            transition: var(--transition);
            box-shadow: 0 3px 8px rgba(39, 174, 96, 0.3);
        }

        .lang-btn:hover {
            background-color: #229b54;
            transform: translateY(-2px);
        }

        .main-menu {
            display: flex;
            gap: 15px;
            margin-bottom: 25px;
            flex-wrap: wrap;
        }

        .menu-btn {
            padding: 14px 20px;
            background-color: var(--secondary);
            color: var(--white);
            border: none;
            border-radius: 10px;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            font-size: 1.05rem;
            font-weight: 600;
            flex: 1;
            min-width: 160px;
            transition: var(--transition);
            box-shadow: var(--shadow);
        }

        .menu-btn:hover {
            background-color: var(--primary);
            transform: translateY(-3px);
        }

        .menu-btn i {
            font-size: 1.3rem;
        }

        .card {
            background-color: var(--white);
            border-radius: var(--border-radius);
            box-shadow: var(--shadow);
            padding: 25px;
            margin-bottom: 25px;
            transition: var(--transition);
        }

        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 30px rgba(0,0,0,0.15);
        }

        h2 {
            margin-bottom: 20px;
            color: var(--secondary);
            font-size: 1.4rem;
            text-align: center;
            font-weight: 700;
        }

        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: var(--secondary);
            font-size: 1.05rem;
        }

        input[type="text"],
        input[type="date"],
        textarea,
        select,
        input[type="file"] {
            width: 100%;
            padding: 14px;
            border: 1px solid #ddd;
            border-radius: 10px;
            font-size: 1.05rem;
            transition: var(--transition);
            font-family: 'Cairo', sans-serif;
        }

        input[type="text"]:focus,
        input[type="date"]:focus,
        textarea:focus {
            border-color: var(--primary);
            outline: none;
            box-shadow: 0 0 0 3px rgba(39, 174, 96, 0.1);
        }

        textarea {
            height: 140px;
            resize: vertical;
            line-height: 1.6;
        }

        .form-row {
            display: flex;
            gap: 20px;
            margin-bottom: 20px;
        }

        .form-row .form-group {
            flex: 1;
        }

        .camera-section {
            margin: 30px 0;
            text-align: center;
        }

        #camera-preview {
            width: 100%;
            max-width: 450px;
            height: auto;
            max-height: 320px;
            background-color: #eee;
            border: 2px dashed #ccc;
            border-radius: 12px;
            margin: 15px auto;
            display: block;
            object-fit: cover;
        }

        .image-actions {
            display: flex;
            justify-content: center;
            gap: 15px;
            flex-wrap: wrap;
            margin: 15px 0;
        }

        #capture-btn,
        .upload-btn {
            padding: 14px 24px;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            font-size: 1.05rem;
            font-weight: 600;
            display: inline-flex;
            align-items: center;
            gap: 10px;
            transition: var(--transition);
            box-shadow: 0 4px 12px rgba(0,0,0,0.15);
        }

        #capture-btn {
            background-color: var(--primary);
            color: var(--white);
        }

        .upload-btn {
            background-color: #3498db;
            color: var(--white);
        }

        #capture-btn:hover,
        .upload-btn:hover {
            transform: translateY(-2px);
        }

        #file-upload {
            display: none;
        }

        #captured-images {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            margin-top: 20px;
            justify-content: center;
            min-height: 60px;
        }

        .image-container {
            position: relative;
            width: 130px;
            height: 130px;
            border-radius: 12px;
            overflow: hidden;
            box-shadow: 0 3px 10px rgba(0,0,0,0.15);
            border: 2px solid var(--primary);
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
            background-color: var(--danger);
            color: var(--white);
            border: none;
            border-radius: 50%;
            width: 32px;
            height: 32px;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            font-size: 0.9rem;
            box-shadow: 0 2px 6px rgba(0,0,0,0.2);
        }

        .delete-image:hover {
            background-color: #c0392b;
        }

        #submit-btn {
            padding: 16px 40px;
            background: linear-gradient(135deg, var(--primary), #219653);
            color: var(--white);
            border: none;
            border-radius: 12px;
            cursor: pointer;
            font-size: 1.2rem;
            font-weight: 700;
            display: block;
            margin: 30px auto;
            transition: var(--transition);
            box-shadow: 0 6px 20px rgba(39, 174, 96, 0.4);
            min-width: 220px;
        }

        #submit-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 25px rgba(39, 174, 96, 0.5);
        }

        /* --- جدول السجلات --- */
        .records-table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
            font-size: 1rem;
            box-shadow: 0 2px 10px rgba(0,0,0,0.05);
            border-radius: 10px;
            overflow: hidden;
        }

        .records-table th {
            background-color: var(--secondary);
            color: var(--white);
            padding: 16px 12px;
            text-align: right;
            font-weight: 600;
        }

        .records-table td {
            padding: 14px 12px;
            border-bottom: 1px solid #eee;
            text-align: right;
        }

        .records-table tr:hover {
            background-color: #f8f9fa;
            transition: var(--transition);
        }

        .action-btn {
            padding: 10px 14px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            margin: 0 4px;
            display: inline-flex;
            align-items: center;
            gap: 6px;
            font-size: 0.95rem;
            font-weight: 600;
            transition: var(--transition);
        }

        .edit-btn {
            background-color: #3498db;
            color: var(--white);
        }

        .delete-btn {
            background-color: var(--danger);
            color: var(--white);
        }

        .pdf-btn {
            background-color: #8e44ad;
            color: var(--white);
        }

        .action-btn:hover {
            transform: scale(1.05);
        }

        .pagination {
            display: flex;
            justify-content: center;
            margin-top: 30px;
            gap: 10px;
            flex-wrap: wrap;
        }

        .page-btn {
            padding: 12px 18px;
            background-color: var(--secondary);
            color: var(--white);
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: 1.05rem;
            min-width: 50px;
            transition: var(--transition);
        }

        .page-btn.active {
            background-color: var(--primary);
            transform: scale(1.08);
        }

        .search-container {
            margin-bottom: 25px;
            display: flex;
            gap: 12px;
            flex-wrap: wrap;
        }

        .search-input {
            flex: 1;
            min-width: 220px;
            padding: 14px;
            border: 1px solid #ddd;
            border-radius: 10px;
            font-size: 1.05rem;
            transition: var(--transition);
        }

        .search-btn {
            padding: 14px 24px;
            background-color: var(--secondary);
            color: var(--white);
            border: none;
            border-radius: 10px;
            cursor: pointer;
            font-weight: 600;
            transition: var(--transition);
        }

        .no-records {
            text-align: center;
            padding: 50px 20px;
            color: #777;
            font-size: 1.2rem;
            background-color: #f9f9f9;
            border-radius: 10px;
            margin: 20px 0;
        }

        .detail-row {
            display: flex;
            margin-bottom: 16px;
            padding-bottom: 6px;
            border-bottom: 1px dashed #eee;
        }

        .detail-label {
            font-weight: 700;
            width: 180px;
            color: var(--secondary);
            flex-shrink: 0;
        }

        .detail-value {
            flex: 1;
            word-wrap: break-word;
            color: #2c3e50;
        }

        .detail-images {
            display: flex;
            flex-wrap: wrap;
            gap: 18px;
            margin-top: 25px;
            justify-content: center;
        }

        .detail-image {
            width: 200px;
            height: 200px;
            object-fit: cover;
            border-radius: 12px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.15);
            border: 2px solid var(--primary);
        }

        .back-btn {
            padding: 12px 24px;
            background-color: #7f8c8d;
            color: var(--white);
            border: none;
            border-radius: 10px;
            cursor: pointer;
            margin-bottom: 25px;
            display: inline-flex;
            align-items: center;
            gap: 10px;
            font-weight: 600;
            transition: var(--transition);
        }

        .back-btn:hover {
            background-color: #95a5a6;
        }

        .hidden {
            display: none !important;
        }

        /* --- تصميم خاص للجوال --- */
        @media (max-width: 768px) {
            .form-row {
                flex-direction: column;
            }
            .header-content {
                text-align: center;
            }
            .menu-btn {
                font-size: 1rem;
                padding: 14px 16px;
                min-width: 140px;
            }
            .records-table th, .records-table td {
                padding: 12px 8px;
                font-size: 0.95rem;
            }
            .action-btn {
                padding: 8px 10px;
                font-size: 0.85rem;
                gap: 4px;
            }
            .image-container, .detail-image {
                width: 100px;
                height: 100px;
            }
            .detail-label {
                width: 140px;
                font-size: 0.95rem;
            }
            #camera-preview {
                max-width: 100%;
            }
            .image-actions {
                flex-direction: column;
                align-items: center;
            }
        }

        @media (max-width: 480px) {
            .container {
                padding: 10px;
            }
            .card {
                padding: 20px;
            }
            h1 {
                font-size: 1.3rem;
            }
            h2 {
                font-size: 1.25rem;
            }
            .menu-btn {
                font-size: 0.95rem;
                padding: 12px 14px;
            }
            .search-container {
                flex-direction: column;
            }
            .search-input, .search-btn {
                width: 100%;
            }
            .detail-image {
                width: 100%;
                height: auto;
            }
            #submit-btn {
                font-size: 1.1rem;
                padding: 14px 30px;
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
                    <button class="lang-btn" onclick="switchLanguage('ar')">العربية</button>
                    <button class="lang-btn" onclick="switchLanguage('en')">English</button>
                </div>
            </div>
        </header>

        <div class="main-menu">
            <button class="menu-btn" onclick="showSection('record-section')">
                <i class="fas fa-plus-circle"></i>
                <span lang="ar">تسجيل إصابة جديدة</span>
                <span lang="en" class="hidden">New Record</span>
            </button>
            <button class="menu-btn" onclick="showSection('records-section')">
                <i class="fas fa-list"></i>
                <span lang="ar">قائمة الإصابات</span>
                <span lang="en" class="hidden">Records List</span>
            </button>
        </div>

        <!-- تسجيل إصابة جديدة -->
        <div class="card" id="record-section">
            <h2 lang="ar">تسجيل إصابة جديدة</h2>
            <h2 lang="en" class="hidden">New Pest/Disease Record</h2>
            <form id="pestForm">
                <div class="form-group">
                    <label lang="ar">تاريخ الاكتشاف</label>
                    <label lang="en" class="hidden">Discovery Date</label>
                    <input type="date" id="discovery-date" required>
                </div>
                <div class="form-row">
                    <div class="form-group">
                        <label lang="ar">اسم الإصابة المحتملة</label>
                        <label lang="en" class="hidden">Potential Pest/Disease Name</label>
                        <input type="text" id="pest-name" placeholder="مثل: منجاة، بق، فطر ..." required>
                    </div>
                    <div class="form-group">
                        <label lang="ar">الاسم العلمي</label>
                        <label lang="en" class="hidden">Scientific Name</label>
                        <input type="text" id="scientific-name" placeholder="مثل: Tetranychus urticae">
                    </div>
                </div>
                <div class="form-group">
                    <label lang="ar">المحصول المصاب</label>
                    <label lang="en" class="hidden">Affected Crop</label>
                    <input type="text" id="affected-crop" placeholder="مثل: طماطم، قمح، برتقال ..." required>
                </div>
                <div class="form-group">
                    <label lang="ar">أعراض الإصابة</label>
                    <label lang="en" class="hidden">Symptoms</label>
                    <textarea id="symptoms" placeholder="صف الأعراض بدقة: لون الأوراق، وجود بقع، تجعد، يبس ..." required></textarea>
                </div>

                <div class="camera-section">
                    <h3 lang="ar">إضافة صور للإصابة</h3>
                    <h3 lang="en" class="hidden">Add Images of the Pest</h3>
                    <video id="camera-preview" autoplay playsinline muted></video>
                    <div class="image-actions">
                        <button type="button" id="capture-btn" onclick="captureImage()">
                            <i class="fas fa-camera"></i>
                            <span lang="ar">التقاط صورة</span>
                            <span lang="en" class="hidden">Capture</span>
                        </button>
                        <label for="file-upload" class="upload-btn">
                            <i class="fas fa-upload"></i>
                            <span lang="ar">اختر من الجهاز</span>
                            <span lang="en" class="hidden">Upload</span>
                        </label>
                        <input type="file" id="file-upload" accept="image/*" multiple onchange="handleFileSelect(event)">
                    </div>
                    <div id="captured-images"></div>
                </div>

                <div class="form-group">
                    <label lang="ar">اسم المبيد (إن وُجد)</label>
                    <label lang="en" class="hidden">Pesticide Name (if any)</label>
                    <input type="text" id="pesticide" placeholder="مثل: أكترا، كارازين ...">
                </div>
                <div class="form-group">
                    <label lang="ar">ملاحظات إضافية</label>
                    <label lang="en" class="hidden">Additional Notes</label>
                    <textarea id="notes" placeholder="ملاحظات حول الموقع، الكثافة، الطقس ..."></textarea>
                </div>
                <button type="submit" id="submit-btn">
                    <i class="fas fa-save"></i>
                    <span lang="ar">حفظ البيانات</span>
                    <span lang="en" class="hidden">Save Record</span>
                </button>
            </form>
        </div>

        <!-- قائمة السجلات -->
        <div class="card hidden" id="records-section">
            <h2 lang="ar">قائمة الإصابات</h2>
            <h2 lang="en" class="hidden">Records List</h2>
            <div class="search-container">
                <input type="text" class="search-input" id="search-input" placeholder="ابحث في السجلات..." lang="ar">
                <input type="text" class="search-input hidden" id="search-input-en" placeholder="Search records..." lang="en">
                <button class="search-btn" onclick="searchRecords()">
                    <i class="fas fa-search"></i>
                    <span lang="ar">بحث</span>
                    <span lang="en" class="hidden">Search</span>
                </button>
            </div>
            <table class="records-table">
                <thead>
                    <tr>
                        <th lang="ar">التاريخ</th>
                        <th lang="en" class="hidden">Date</th>
                        <th lang="ar">الإصابة</th>
                        <th lang="en" class="hidden">Pest/Disease</th>
                        <th lang="ar">المحصول</th>
                        <th lang="en" class="hidden">Crop</th>
                        <th lang="ar">الإجراءات</th>
                        <th lang="en" class="hidden">Actions</th>
                    </tr>
                </thead>
                <tbody id="records-table-body"></tbody>
            </table>
            <div class="no-records hidden" id="no-records">
                <p lang="ar">لا توجد سجلات مسجلة</p>
                <p lang="en" class="hidden">No records found</p>
            </div>
            <div class="pagination" id="pagination"></div>
        </div>

        <!-- تفاصيل السجل -->
        <div class="card hidden" id="record-details-section">
            <button class="back-btn" onclick="showSection('records-section')">
                <i class="fas fa-arrow-left"></i>
                <span lang="ar">العودة للقائمة</span>
                <span lang="en" class="hidden">Back to List</span>
            </button>
            <h2 lang="ar">تفاصيل السجل</h2>
            <h2 lang="en" class="hidden">Record Details</h2>
            <div id="record-details"></div>
        </div>
    </div>

    <script>
        // تضمين خط عربي بصيغة Base64 (Cairo)
        const cairoFontBase64 = `UyvGjQUAAAAAAADKqAAAAAAAAAABAAEAAAAARFNQVAAAAEwAAAD8AAAAIgAAAAQAAAAEAAAClAAAABQAAAKkAAAAEgAAApwAAAAEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA......`; // (تم تقصيره للعرض)

        // المتغيرات
        let currentLanguage = 'ar';
        let records = JSON.parse(localStorage.getItem('pestRecords')) || [];
        let currentPage = 1;
        const recordsPerPage = 5;
        let stream = null;

        // تهيئة عند التحميل
        document.addEventListener('DOMContentLoaded', () => {
            const today = new Date().toISOString().split('T')[0];
            document.getElementById('discovery-date').value = today;

            initCamera();
            showSection('record-section');
            if (records.length > 0) renderRecordsTable();
            else document.getElementById('no-records').classList.remove('hidden');

            // تهيئة jsPDF مع خط عربي
            window.jsPDF = window.jspdf.jsPDF;
            jsPDF.API.events.push(['addFonts', function() {
                this.addFileToVFS('Cairo-Regular.ttf', cairoFontBase64.split(',')[1]);
                this.addFont('Cairo-Regular.ttf', 'Cairo', 'normal');
            }]);
        });

        // تبديل اللغة
        function switchLanguage(lang) {
            currentLanguage = lang;
            document.querySelectorAll('[lang]').forEach(el => el.classList.add('hidden'));
            document.querySelectorAll(`[lang="${lang}"]`).forEach(el => el.classList.remove('hidden'));
            document.documentElement.lang = lang;
            document.documentElement.dir = lang === 'ar' ? 'rtl' : 'ltr';
            document.body.style.fontFamily = lang === 'ar' ? "'Cairo', sans-serif" : "Arial, sans-serif";
            if (!document.getElementById('records-section').classList.contains('hidden')) renderRecordsTable();
        }

        // عرض قسم معين
        function showSection(id) {
            document.querySelectorAll('.card').forEach(s => s.classList.add('hidden'));
            document.getElementById(id).classList.remove('hidden');
            if (id === 'records-section') renderRecordsTable();
        }

        // تهيئة الكاميرا
        async function initCamera() {
            try {
                stream = await navigator.mediaDevices.getUserMedia({ video: { facingMode: 'environment' } });
                document.getElementById('camera-preview').srcObject = stream;
            } catch (err) {
                console.error("Camera error:", err);
                const preview = document.getElementById('camera-preview');
                preview.src = '';
                preview.style.backgroundColor = '#f0f0f0';
                preview.style.border = '2px dashed #ccc';
            }
        }

        // التقاط صورة
        function captureImage() {
            const video = document.getElementById('camera-preview');
            if (!video.srcObject) return alert('الكاميرا غير متاحة');
            const canvas = document.createElement('canvas');
            canvas.width = 640;
            canvas.height = 480;
            const ctx = canvas.getContext('2d');
            ctx.drawImage(video, 0, 0, canvas.width, canvas.height);
            const imgData = canvas.toDataURL('image/jpeg', 0.9);
            addImageToContainer(imgData);
        }

        // رفع صور من الجهاز
        function handleFileSelect(e) {
            Array.from(e.target.files).forEach(file => {
                const reader = new FileReader();
                reader.onload = (event) => addImageToContainer(event.target.result);
                reader.readAsDataURL(file);
            });
        }

        // إضافة صورة
        function addImageToContainer(src) {
            const div = document.createElement('div');
            div.className = 'image-container';
            div.innerHTML = `
                <img src="${src}" alt="Image">
                <button class="delete-image" onclick="this.parentElement.remove()"><i class="fas fa-times"></i></button>
            `;
            document.getElementById('captured-images').appendChild(div);
        }

        // حفظ السجل
        document.getElementById('pestForm').addEventListener('submit', function(e) {
            e.preventDefault();
            const form = this;
            const formData = {
                id: Date.now().toString(),
                date: form['discovery-date'].value,
                pestName: form['pest-name'].value,
                scientificName: form['scientific-name'].value,
                affectedCrop: form['affected-crop'].value,
                symptoms: form['symptoms'].value,
                pesticide: form['pesticide'].value,
                notes: form['notes'].value,
                images: Array.from(document.querySelectorAll('#captured-images img')).map(img => img.src),
                createdAt: new Date().toISOString()
            };
            records.unshift(formData);
            localStorage.setItem('pestRecords', JSON.stringify(records));
            alert('تم حفظ السجل بنجاح!');
            form.reset();
            document.getElementById('discovery-date').value = new Date().toISOString().split('T')[0];
            document.getElementById('captured-images').innerHTML = '';
            showSection('records-section');
        });

        // عرض الجدول
        function renderRecordsTable(page = 1) {
            currentPage = page;
            const start = (page - 1) * recordsPerPage;
            const data = records.slice(start, start + recordsPerPage);
            const tbody = document.getElementById('records-table-body');
            tbody.innerHTML = '';

            if (data.length === 0) {
                document.getElementById('no-records').classList.remove('hidden');
                document.getElementById('pagination').innerHTML = '';
                return;
            } else {
                document.getElementById('no-records').classList.add('hidden');
            }

            data.forEach(r => {
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td>${r.date}</td>
                    <td>${r.pestName}</td>
                    <td>${r.affectedCrop}</td>
                    <td>
                        <button class="action-btn" onclick="viewRecord('${r.id}')"><i class="fas fa-eye"></i></button>
                        <button class="action-btn edit-btn" onclick="editRecord('${r.id}')"><i class="fas fa-edit"></i></button>
                        <button class="action-btn delete-btn" onclick="deleteRecord('${r.id}')"><i class="fas fa-trash"></i></button>
                        <button class="action-btn pdf-btn" onclick="generatePDF('${r.id}')"><i class="fas fa-file-pdf"></i></button>
                    </td>
                `;
                tbody.appendChild(row);
            });
            renderPagination();
        }

        function renderPagination() {
            const pages = Math.ceil(records.length / recordsPerPage);
            const div = document.getElementById('pagination');
            div.innerHTML = '';
            if (pages <= 1) return;
            for (let i = 1; i <= pages; i++) {
                const btn = document.createElement('button');
                btn.className = `page-btn ${i === currentPage ? 'active' : ''}`;
                btn.textContent = i;
                btn.onclick = () => renderRecordsTable(i);
                div.appendChild(btn);
            }
        }

        function viewRecord(id) {
            const r = records.find(r => r.id === id);
            if (!r) return;
            document.getElementById('record-details').innerHTML = `
                <div class="detail-row"><div class="detail-label" lang="ar">التاريخ:</div><div class="detail-value">${r.date}</div></div>
                <div class="detail-row"><div class="detail-label" lang="ar">الإصابة:</div><div class="detail-value">${r.pestName}</div></div>
                <div class="detail-row"><div class="detail-label" lang="ar">الاسم العلمي:</div><div class="detail-value">${r.scientificName || '—'}</div></div>
                <div class="detail-row"><div class="detail-label" lang="ar">المحصول:</div><div class="detail-value">${r.affectedCrop}</div></div>
                <div class="detail-row"><div class="detail-label" lang="ar">الأعراض:</div><div class="detail-value">${r.symptoms}</div></div>
                <div class="detail-row"><div class="detail-label" lang="ar">المبيد:</div><div class="detail-value">${r.pesticide || '—'}</div></div>
                <div class="detail-row"><div class="detail-label" lang="ar">ملاحظات:</div><div class="detail-value">${r.notes || '—'}</div></div>
                <h3 lang="ar">صور الإصابة:</h3>
                <div class="detail-images">${r.images.map(s => `<img src="${s}" class="detail-image">`).join('') || 'لا توجد صور'}</div>
            `;
            switchLanguage(currentLanguage);
            showSection('record-details-section');
        }

        function generatePDF(id) {
            const r = records.find(r => r.id === id);
            if (!r) return;
            const { jsPDF } = window.jspdf;
            const doc = new jsPDF({
                orientation: 'portrait',
                unit: 'mm',
                format: 'a4'
            });

            // استخدام الخط العربي
            doc.setFont('Cairo');

            doc.setFontSize(20);
            doc.setTextColor(40, 40, 40);
            doc.text('تقرير الإصابة النباتية', 105, 20, { align: 'center' });

            doc.setFontSize(14);
            let y = 40;

            const left = 20;
            const maxWidth = 170;

            doc.text(`تاريخ الاكتشاف: ${r.date}`, left, y); y += 15;
            doc.text(`اسم الإصابة: ${r.pestName}`, left, y); y += 15;
            if (r.scientificName) {
                doc.text(`الاسم العلمي: ${r.scientificName}`, left, y); y += 15;
            }
            doc.text(`المحصول: ${r.affectedCrop}`, left, y); y += 15;

            doc.text('الأعراض:', left, y); y += 8;
            const symptoms = doc.splitTextToSize(r.symptoms, maxWidth);
            doc.text(symptoms, left, y); y += symptoms.length * 6 + 10;

            if (r.pesticide) {
                doc.text(`اسم المبيد: ${r.pesticide}`, left, y); y += 15;
            }
            if (r.notes) {
                doc.text('ملاحظات:', left, y); y += 8;
                const notes = doc.splitTextToSize(r.notes, maxWidth);
                doc.text(notes, left, y); y += notes.length * 6 + 10;
            }

            if (r.images && r.images.length > 0) {
                doc.addPage();
                doc.text('صور الإصابة', left, 20);
                y = 30;
                r.images.forEach((img, i) => {
                    if (i > 0 && i % 2 === 0) {
                        doc.addPage();
                        y = 30;
                    }
                    if (i % 2 === 1) y = 120;
                    doc.addImage(img, 'JPEG', 20, y, 80, 80);
                    if (i % 2 === 0 && i < r.images.length - 1) {
                        doc.addImage(r.images[i + 1], 'JPEG', 110, y, 80, 80);
                    }
                    y += 90;
                });
            }

            doc.save(`${r.pestName}_${r.date}.pdf`);
        }

        function editRecord(id) {
            const r = records.find(r => r.id === id);
            if (!r) return;
            document.getElementById('discovery-date').value = r.date;
            document.getElementById('pest-name').value = r.pestName;
            document.getElementById('scientific-name').value = r.scientificName || '';
            document.getElementById('affected-crop').value = r.affectedCrop;
            document.getElementById('symptoms').value = r.symptoms;
            document.getElementById('pesticide').value = r.pesticide || '';
            document.getElementById('notes').value = r.notes || '';

            const container = document.getElementById('captured-images');
            container.innerHTML = '';
            (r.images || []).forEach(src => addImageToContainer(src));

            records = records.filter(r => r.id !== id);
            localStorage.setItem('pestRecords', JSON.stringify(records));
            showSection('record-section');
        }

        function deleteRecord(id) {
            if (confirm('هل أنت متأكد من الحذف؟')) {
                records = records.filter(r => r.id !== id);
                localStorage.setItem('pestRecords', JSON.stringify(records));
                renderRecordsTable();
                if (records.length === 0) document.getElementById('no-records').classList.remove('hidden');
            }
        }

        function searchRecords() {
            const term = (currentLanguage === 'ar' ? document.getElementById('search-input') : document.getElementById('search-input-en')).value.toLowerCase().trim();
            if (!term) return renderRecordsTable();
            const results = records.filter(r =>
                r.pestName.toLowerCase().includes(term) ||
                (r.scientificName && r.scientificName.toLowerCase().includes(term)) ||
                r.affectedCrop.toLowerCase().includes(term) ||
                r.symptoms.toLowerCase().includes(term) ||
                (r.pesticide && r.pesticide.toLowerCase().includes(term)) ||
                (r.notes && r.notes.toLowerCase().includes(term))
            );
            renderSearchResults(results);
        }

        function renderSearchResults(results) {
            const tbody = document.getElementById('records-table-body');
            tbody.innerHTML = results.length ? results.map(r => `
                <tr>
                    <td>${r.date}</td>
                    <td>${r.pestName}</td>
                    <td>${r.affectedCrop}</td>
                    <td>
                        <button class="action-btn" onclick="viewRecord('${r.id}')"><i class="fas fa-eye"></i></button>
                        <button class="action-btn edit-btn" onclick="editRecord('${r.id}')"><i class="fas fa-edit"></i></button>
                        <button class="action-btn delete-btn" onclick="deleteRecord('${r.id}')"><i class="fas fa-trash"></i></button>
                        <button class="action-btn pdf-btn" onclick="generatePDF('${r.id}')"><i class="fas fa-file-pdf"></i></button>
                    </td>
                </tr>
            `).join('') : '';
            document.getElementById('no-records').classList.add('hidden');
            document.getElementById('pagination').innerHTML = '';
        }
    </script>
</body>
</html>
