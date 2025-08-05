<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>نظام تسجيل الآفات والأمراض النباتية</title>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
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
            --border-radius: 16px;
            --shadow: 0 6px 25px rgba(0,0,0,0.12);
            --transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            --btn-size: 56px;
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
            line-height: 1.7;
            direction: rtl;
            -webkit-font-smoothing: antialiased;
            -moz-osx-font-smoothing: grayscale;
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
            padding: 20px 0;
            border-radius: var(--border-radius) var(--border-radius) 0 0;
            margin-bottom: 25px;
            box-shadow: var(--shadow);
        }
        .header-content {
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 0 20px;
        }
        h1 {
            font-size: 1.6rem;
            font-weight: 700;
            text-shadow: 1px 1px 4px rgba(0,0,0,0.3);
        }
        .main-menu {
            display: flex;
            gap: 20px;
            margin-bottom: 30px;
            flex-wrap: wrap;
        }
        .menu-btn {
            padding: 18px 25px;
            background-color: var(--secondary);
            color: var(--white);
            border: none;
            border-radius: 14px;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 12px;
            font-size: 1.15rem;
            font-weight: 600;
            flex: 1;
            min-width: 180px;
            transition: var(--transition);
            box-shadow: var(--shadow);
            height: var(--btn-size);
        }
        .menu-btn:hover {
            background-color: var(--primary);
            transform: translateY(-4px);
            box-shadow: 0 8px 30px rgba(39, 174, 96, 0.4);
        }
        .menu-btn i {
            font-size: 1.4rem;
        }
        .card {
            background-color: var(--white);
            border-radius: var(--border-radius);
            box-shadow: var(--shadow);
            padding: 30px;
            margin-bottom: 30px;
            transition: var(--transition);
        }
        .card:hover {
            transform: translateY(-6px);
            box-shadow: 0 12px 40px rgba(0,0,0,0.18);
        }
        h2 {
            margin-bottom: 25px;
            color: var(--secondary);
            font-size: 1.5rem;
            text-align: center;
            font-weight: 700;
            padding-bottom: 15px;
            border-bottom: 2px solid var(--primary);
        }
        label {
            display: block;
            margin-bottom: 12px;
            font-weight: 600;
            color: var(--secondary);
            font-size: 1.1rem;
        }
        input[type="text"],
        input[type="date"],
        textarea,
        select,
        input[type="file"] {
            width: 100%;
            padding: 18px 16px;
            border: 2px solid #ddd;
            border-radius: 12px;
            font-size: 1.1rem;
            transition: var(--transition);
            font-family: 'Cairo', sans-serif;
            min-height: 56px;
        }
        input[type="text"]:focus,
        input[type="date"]:focus,
        textarea:focus {
            border-color: var(--primary);
            outline: none;
            box-shadow: 0 0 0 4px rgba(39, 174, 96, 0.15);
            transform: scale(1.02);
        }
        textarea {
            min-height: 160px;
            resize: vertical;
            line-height: 1.7;
        }
        .form-row {
            display: flex;
            gap: 25px;
            margin-bottom: 25px;
        }
        .form-row .form-group {
            flex: 1;
        }
        .camera-section {
            margin: 35px 0;
            text-align: center;
        }
        #camera-preview {
            width: 100%;
            max-width: 500px;
            height: auto;
            max-height: 360px;
            background-color: #eee;
            border: 3px dashed #ccc;
            border-radius: 16px;
            margin: 20px auto;
            display: block;
            object-fit: cover;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
        }
        .image-actions {
            display: flex;
            justify-content: center;
            gap: 20px;
            flex-wrap: wrap;
            margin: 20px 0;
        }
        #capture-btn,
        .upload-btn {
            padding: 16px 28px;
            border: none;
            border-radius: 14px;
            cursor: pointer;
            font-size: 1.1rem;
            font-weight: 600;
            display: inline-flex;
            align-items: center;
            gap: 12px;
            transition: var(--transition);
            box-shadow: 0 6px 18px rgba(0,0,0,0.18);
            min-height: 60px;
            min-width: 180px;
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
            transform: translateY(-3px);
        }
        #file-upload {
            display: none;
        }
        #captured-images {
            display: flex;
            flex-wrap: wrap;
            gap: 16px;
            margin-top: 25px;
            justify-content: center;
            min-height: 80px;
        }
        .image-container {
            position: relative;
            width: 150px;
            height: 150px;
            border-radius: 16px;
            overflow: hidden;
            box-shadow: 0 5px 20px rgba(0,0,0,0.15);
            border: 3px solid var(--primary);
            transition: var(--transition);
        }
        .image-container:hover {
            transform: scale(1.08);
            box-shadow: 0 8px 30px rgba(0,0,0,0.2);
        }
        .image-container img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: var(--transition);
        }
        .image-container img:hover {
            transform: scale(1.1);
        }
        .delete-image {
            position: absolute;
            top: 10px;
            right: 10px;
            background-color: var(--danger);
            color: var(--white);
            border: none;
            border-radius: 50%;
            width: 36px;
            height: 36px;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            font-size: 1rem;
            box-shadow: 0 3px 8px rgba(0,0,0,0.2);
            opacity: 0;
            transition: var(--transition);
        }
        .image-container:hover .delete-image {
            opacity: 1;
        }
        .delete-image:hover {
            background-color: #c0392b;
            transform: scale(1.15);
        }
        #submit-btn {
            padding: 18px 50px;
            background: linear-gradient(135deg, var(--primary), #219653);
            color: var(--white);
            border: none;
            border-radius: 16px;
            cursor: pointer;
            font-size: 1.3rem;
            font-weight: 700;
            display: block;
            margin: 35px auto;
            transition: var(--transition);
            box-shadow: 0 8px 25px rgba(39, 174, 96, 0.5);
            min-width: 250px;
            min-height: 70px;
        }
        #submit-btn:hover {
            transform: translateY(-4px);
            box-shadow: 0 12px 35px rgba(39, 174, 96, 0.6);
        }
        /* --- جدول السجلات --- */
        .records-table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 25px;
            font-size: 1.1rem;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
            border-radius: 12px;
            overflow: hidden;
        }
        .records-table th {
            background-color: var(--secondary);
            color: var(--white);
            padding: 20px 15px;
            text-align: right;
            font-weight: 600;
            font-size: 1.15rem;
        }
        .records-table td {
            padding: 18px 15px;
            border-bottom: 1px solid #eee;
            text-align: right;
            font-size: 1.05rem;
        }
        .records-table tr:hover {
            background-color: #f8f9fa;
            transition: var(--transition);
        }
        .action-btn {
            padding: 14px 18px;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            margin: 0 6px;
            display: inline-flex;
            align-items: center;
            gap: 8px;
            font-size: 1.05rem;
            font-weight: 600;
            transition: var(--transition);
            min-height: 50px;
            min-width: 50px;
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
            transform: scale(1.1);
        }
        .pagination {
            display: flex;
            justify-content: center;
            margin-top: 35px;
            gap: 12px;
            flex-wrap: wrap;
        }
        .page-btn {
            padding: 14px 20px;
            background-color: var(--secondary);
            color: var(--white);
            border: none;
            border-radius: 10px;
            cursor: pointer;
            font-size: 1.1rem;
            min-width: 60px;
            transition: var(--transition);
            min-height: 56px;
        }
        .page-btn.active {
            background-color: var(--primary);
            transform: scale(1.12);
        }
        .search-container {
            margin-bottom: 30px;
            display: flex;
            gap: 15px;
            flex-wrap: wrap;
        }
        .search-input {
            flex: 1;
            min-width: 250px;
            padding: 16px 18px;
            border: 2px solid #ddd;
            border-radius: 12px;
            font-size: 1.1rem;
            transition: var(--transition);
            min-height: 60px;
        }
        .search-btn {
            padding: 16px 28px;
            background-color: var(--secondary);
            color: var(--white);
            border: none;
            border-radius: 12px;
            cursor: pointer;
            font-weight: 600;
            transition: var(--transition);
            min-height: 60px;
            min-width: 120px;
        }
        .no-records {
            text-align: center;
            padding: 60px 30px;
            color: #777;
            font-size: 1.3rem;
            background: linear-gradient(135deg, #f8f9fa, #e9ecef);
            border-radius: 12px;
            margin: 25px 0;
            border: 2px dashed #dee2e6;
        }
        .detail-row {
            display: flex;
            margin-bottom: 20px;
            padding-bottom: 10px;
            border-bottom: 1px dashed #eee;
        }
        .detail-label {
            font-weight: 700;
            width: 200px;
            color: var(--secondary);
            flex-shrink: 0;
            font-size: 1.1rem;
        }
        .detail-value {
            flex: 1;
            word-wrap: break-word;
            color: #2c3e50;
            font-size: 1.1rem;
        }
        .detail-images {
            display: flex;
            flex-wrap: wrap;
            gap: 20px;
            margin-top: 30px;
            justify-content: center;
        }
        .detail-image {
            width: 250px;
            height: 250px;
            object-fit: cover;
            border-radius: 16px;
            box-shadow: 0 8px 25px rgba(0,0,0,0.18);
            border: 3px solid var(--primary);
            transition: var(--transition);
        }
        .detail-image:hover {
            transform: scale(1.08);
            box-shadow: 0 12px 40px rgba(0,0,0,0.25);
        }
        .back-btn {
            padding: 14px 28px;
            background-color: #7f8c8d;
            color: var(--white);
            border: none;
            border-radius: 12px;
            cursor: pointer;
            margin-bottom: 30px;
            display: inline-flex;
            align-items: center;
            gap: 12px;
            font-weight: 600;
            transition: var(--transition);
            min-height: 56px;
            min-width: 160px;
        }
        .back-btn:hover {
            background-color: #95a5a6;
            transform: translateY(-3px);
        }
        .hidden {
            display: none !important;
        }
        @media (max-width: 768px) {
            .form-row {
                flex-direction: column;
            }
            .header-content {
                text-align: center;
            }
            .menu-btn {
                font-size: 1.1rem;
                padding: 16px 20px;
                min-width: 160px;
            }
            .records-table th, .records-table td {
                padding: 16px 12px;
                font-size: 1.05rem;
            }
            .action-btn {
                padding: 12px 16px;
                font-size: 1rem;
                gap: 6px;
            }
            .image-container, .detail-image {
                width: 120px;
                height: 120px;
            }
            .detail-label {
                width: 160px;
                font-size: 1.05rem;
            }
            #camera-preview {
                max-width: 100%;
            }
            .image-actions {
                flex-direction: column;
                align-items: center;
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
                font-size: 1.2rem;
                padding: 16px 40px;
            }
        }
        @media (max-width: 480px) {
            .container {
                padding: 12px;
            }
            .card {
                padding: 25px;
            }
            h1 {
                font-size: 1.4rem;
            }
            h2 {
                font-size: 1.35rem;
            }
            .menu-btn {
                font-size: 1rem;
                padding: 14px 18px;
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
                font-size: 1.15rem;
                padding: 16px 35px;
                min-width: 220px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <div class="header-content">
                <h1>نظام تسجيل الآفات والأمراض النباتية</h1>
            </div>
        </header>
        <div class="main-menu">
            <button class="menu-btn" onclick="showSection('record-section')">
                <i class="fas fa-plus-circle"></i>
                تسجيل إصابة جديدة
            </button>
            <button class="menu-btn" onclick="showSection('records-section')">
                <i class="fas fa-list"></i>
                قائمة الإصابات
            </button>
        </div>
        <!-- تسجيل إصابة جديدة -->
        <div class="card" id="record-section">
            <h2>تسجيل إصابة جديدة</h2>
            <form id="pestForm">
                <div class="form-group">
                    <label>تاريخ الاكتشاف</label>
                    <input type="date" id="discovery-date" required>
                </div>
                <div class="form-group">
                    <label>اسم مدخل البيانات</label>
                    <input type="text" id="recorded-by" placeholder="اسم الشخص الذي سجل البيانات" required>
                </div>
                <div class="form-group">
                    <label>الموقع</label>
                    <input type="text" id="location" placeholder="اسم الحقلة، المنطقة، المحافظة ..." required>
                </div>
                <div class="form-row">
                    <div class="form-group">
                        <label>اسم الإصابة المحتملة</label>
                        <input type="text" id="pest-name" placeholder="مثل: منجاة، بق، فطر ..." required>
                    </div>
                    <div class="form-group">
                        <label>الاسم العلمي</label>
                        <input type="text" id="scientific-name" placeholder="مثل: Tetranychus urticae">
                    </div>
                </div>
                <div class="form-group">
                    <label>المحصول المصاب</label>
                    <input type="text" id="affected-crop" placeholder="مثل: طماطم، قمح، برتقال ..." required>
                </div>
                <div class="form-group">
                    <label>أعراض الإصابة</label>
                    <textarea id="symptoms" placeholder="صف الأعراض بدقة: لون الأوراق، وجود بقع، تجعد، يبس ..." required></textarea>
                </div>
                <div class="camera-section">
                    <h3>إضافة صور للإصابة</h3>
                    <video id="camera-preview" autoplay playsinline muted></video>
                    <div class="image-actions">
                        <button type="button" id="capture-btn" onclick="captureImage()">
                            <i class="fas fa-camera"></i>
                            التقاط صورة
                        </button>
                        <label for="file-upload" class="upload-btn">
                            <i class="fas fa-upload"></i>
                            اختر من الجهاز
                        </label>
                        <input type="file" id="file-upload" accept="image/*" multiple onchange="handleFileSelect(event)">
                    </div>
                    <div id="captured-images"></div>
                </div>
                <div class="form-group">
                    <label>اسم المبيد (إن وُجد)</label>
                    <input type="text" id="pesticide" placeholder="مثل: أكترا، كارازين ...">
                </div>
                <div class="form-group">
                    <label>ملاحظات إضافية</label>
                    <textarea id="notes" placeholder="ملاحظات حول الكثافة، الطقس ..."></textarea>
                </div>
                <button type="submit" id="submit-btn">
                    <i class="fas fa-save"></i>
                    حفظ البيانات
                </button>
            </form>
        </div>
        <!-- قائمة السجلات -->
        <div class="card hidden" id="records-section">
            <h2>قائمة الإصابات</h2>
            <div class="search-container">
                <input type="text" class="search-input" id="search-input" placeholder="ابحث في السجلات...">
                <button class="search-btn" onclick="searchRecords()">
                    <i class="fas fa-search"></i>
                    بحث
                </button>
            </div>
            <table class="records-table">
                <thead>
                    <tr>
                        <th>التاريخ</th>
                        <th>الإصابة</th>
                        <th>المحصول</th>
                        <th>الإجراءات</th>
                    </tr>
                </thead>
                <tbody id="records-table-body"></tbody>
            </table>
            <div class="no-records hidden" id="no-records">
                <p>لا توجد سجلات مسجلة</p>
            </div>
            <div class="pagination" id="pagination"></div>
        </div>
        <!-- تفاصيل السجل -->
        <div class="card hidden" id="record-details-section">
            <button class="back-btn" onclick="showSection('records-section')">
                <i class="fas fa-arrow-left"></i>
                العودة للقائمة
            </button>
            <h2>تفاصيل السجل</h2>
            <div id="record-details"></div>
        </div>
    </div>
    <script>
        // المتغيرات
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
            window.jsPDF = window.jspdf.jsPDF;
        });

        // عرض قسم معين
        function showSection(id) {
            document.querySelectorAll('.card').forEach(s => s.classList.add('hidden'));
            document.getElementById(id).classList.remove('hidden');
            if (id === 'records-section') renderRecordsTable();
        }

        // تهيئة الكاميرا الخلفية
        async function initCamera() {
            try {
                const constraints = {
                    video: { facingMode: { exact: 'environment' } }
                };
                stream = await navigator.mediaDevices.getUserMedia(constraints);
                document.getElementById('camera-preview').srcObject = stream;
            } catch (err) {
                console.error("Camera error:", err);
                try {
                    stream = await navigator.mediaDevices.getUserMedia({ video: true });
                    document.getElementById('camera-preview').srcObject = stream;
                } catch (err2) {
                    console.error("Could not access any camera:", err2);
                    const preview = document.getElementById('camera-preview');
                    preview.src = '';
                    preview.style.backgroundColor = '#f0f0f0';
                    preview.style.border = '3px dashed #ccc';
                }
            }
        }

        // التقاط صورة
        function captureImage() {
            const video = document.getElementById('camera-preview');
            if (!video.srcObject) {
                alert('الكاميرا غير متاحة');
                return;
            }
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
            const files = e.target.files;
            if (!files || files.length === 0) return;
            Array.from(files).forEach(file => {
                const reader = new FileReader();
                reader.onload = function(event) {
                    addImageToContainer(event.target.result);
                };
                reader.readAsDataURL(file);
            });
        }

        // إضافة صورة
        function addImageToContainer(src) {
            if (!src) return;
            const container = document.createElement('div');
            container.className = 'image-container';
            const img = document.createElement('img');
            img.src = src;
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

        // حفظ السجل
        document.getElementById('pestForm').addEventListener('submit', function(e) {
            e.preventDefault();
            const form = this;
            const imageElements = document.querySelectorAll('#captured-images .image-container img');
            const images = Array.from(imageElements).map(img => img.src);
            const formData = {
                id: Date.now().toString(),
                date: form['discovery-date'].value,
                pestName: form['pest-name'].value,
                scientificName: form['scientific-name'].value,
                affectedCrop: form['affected-crop'].value,
                symptoms: form['symptoms'].value,
                pesticide: form['pesticide'].value,
                notes: form['notes'].value,
                recordedBy: form['recorded-by'].value,
                location: form['location'].value,
                images: images,
                createdAt: new Date().toISOString()
            };
            records.unshift(formData);
            try {
                localStorage.setItem('pestRecords', JSON.stringify(records));
                alert('تم حفظ السجل بنجاح!');
            } catch (e) {
                alert('حدث خطأ في حفظ البيانات.');
                return;
            }
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
            const totalPages = Math.ceil(records.length / recordsPerPage);
            const div = document.getElementById('pagination');
            div.innerHTML = '';
            if (totalPages <= 1) return;
            for (let i = 1; i <= totalPages; i++) {
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
                <div class="detail-row"><div class="detail-label">التاريخ:</div><div class="detail-value">${r.date}</div></div>
                <div class="detail-row"><div class="detail-label">اسم مدخل البيانات:</div><div class="detail-value">${r.recordedBy}</div></div>
                <div class="detail-row"><div class="detail-label">الموقع:</div><div class="detail-value">${r.location}</div></div>
                <div class="detail-row"><div class="detail-label">الإصابة:</div><div class="detail-value">${r.pestName}</div></div>
                <div class="detail-row"><div class="detail-label">الاسم العلمي:</div><div class="detail-value">${r.scientificName || '—'}</div></div>
                <div class="detail-row"><div class="detail-label">المحصول:</div><div class="detail-value">${r.affectedCrop}</div></div>
                <div class="detail-row"><div class="detail-label">الأعراض:</div><div class="detail-value">${r.symptoms}</div></div>
                <div class="detail-row"><div class="detail-label">المبيد:</div><div class="detail-value">${r.pesticide || '—'}</div></div>
                <div class="detail-row"><div class="detail-label">ملاحظات:</div><div class="detail-value">${r.notes || '—'}</div></div>
                <h3>صور الإصابة:</h3>
                <div class="detail-images">${r.images && r.images.length > 0 ? r.images.map(s => `<img src="${s}" class="detail-image">`).join('') : 'لا توجد صور'}</div>
            `;
            showSection('record-details-section');
        }

        function generatePDF(id) {
            const r = records.find(r => r.id === id);
            if (!r) return;
            const tempDiv = document.createElement('div');
            tempDiv.style.position = 'absolute';
            tempDiv.style.left = '-9999px';
            tempDiv.style.width = '210mm';
            tempDiv.style.padding = '20px';
            tempDiv.style.fontFamily = "'Cairo', 'Arial', sans-serif";
            tempDiv.style.direction = 'rtl';
            tempDiv.style.backgroundColor = 'white';
            tempDiv.style.fontSize = '14px';
            tempDiv.style.lineHeight = '1.6';
            tempDiv.innerHTML = `
                <div style="text-align: center; margin-bottom: 20px;">
                    <h1 style="color: #2c3e50; font-size: 24px; margin-bottom: 5px; font-weight: 700;">تقرير الإصابة النباتية</h1>
                    <p style="font-size: 16px; color: #555;">تاريخ التقرير: ${new Date().toLocaleDateString()}</p>
                </div>
                <div style="margin-bottom: 20px;">
                    <h3 style="color: #2c3e50; font-size: 18px; border-bottom: 1px solid #eee; padding-bottom: 10px;">معلومات السجل</h3>
                    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 15px; margin-top: 15px;">
                        <div><strong style="color: #2c3e50;">تاريخ الاكتشاف:</strong> ${r.date}</div>
                        <div><strong style="color: #2c3e50;">اسم مدخل البيانات:</strong> ${r.recordedBy}</div>
                        <div><strong style="color: #2c3e50;">الموقع:</strong> ${r.location}</div>
                        <div><strong style="color: #2c3e50;">اسم الإصابة:</strong> ${r.pestName}</div>
                        <div><strong style="color: #2c3e50;">الاسم العلمي:</strong> ${r.scientificName || '-'}</div>
                        <div><strong style="color: #2c3e50;">المحصول المصاب:</strong> ${r.affectedCrop}</div>
                        <div style="grid-column: 1 / 3;"><strong style="color: #2c3e50;">أعراض الإصابة:</strong> ${r.symptoms}</div>
                        <div><strong style="color: #2c3e50;">اسم المبيد:</strong> ${r.pesticide || '-'}</div>
                        <div><strong style="color: #2c3e50;">ملاحظات:</strong> ${r.notes || '-'}</div>
                    </div>
                </div>
                ${r.images && r.images.length > 0 ? `
                <div style="margin-bottom: 20px;">
                    <h3 style="color: #2c3e50; font-size: 18px; border-bottom: 1px solid #eee; padding-bottom: 10px;">صور الإصابة</h3>
                    <div style="display: flex; flex-wrap: wrap; gap: 15px; margin-top: 15px;">
                        ${r.images.map(img => `
                        <div style="flex: 1; min-width: 200px; max-width: 300px;">
                            <img src="${img}" style="width: 100%; height: auto; border-radius: 8px; box-shadow: 0 2px 10px rgba(0,0,0,0.1);">
                        </div>
                        `).join('')}
                    </div>
                </div>
                ` : ''}
                <div style="text-align: center; margin-top: 30px; font-size: 12px; color: #777; border-top: 1px solid #eee; padding-top: 15px;">
                    تم إعداد هذا التقرير من قبل: <strong>${r.recordedBy}</strong>
                </div>
            `;
            document.body.appendChild(tempDiv);
            html2canvas(tempDiv, { scale: 2, useCORS: true, logging: false }).then(canvas => {
                const pdf = new jsPDF({
                    orientation: 'portrait',
                    unit: 'mm',
                    format: 'a4'
                });
                const imgData = canvas.toDataURL('image/jpeg', 0.95);
                const pdfWidth = pdf.internal.pageSize.getWidth();
                const pdfHeight = (canvas.height * pdfWidth) / canvas.width;
                pdf.addImage(imgData, 'JPEG', 0, 0, pdfWidth, pdfHeight);
                pdf.save(`${r.pestName}_${r.date}.pdf`);
            }).catch(error => {
                alert('حدث خطأ أثناء إنشاء الملف.');
            }).finally(() => {
                document.body.removeChild(tempDiv);
            });
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
            document.getElementById('recorded-by').value = r.recordedBy;
            document.getElementById('location').value = r.location;
            const container = document.getElementById('captured-images');
            container.innerHTML = '';
            (r.images || []).forEach(src => addImageToContainer(src));
            records = records.filter(r => r.id !== id);
            try {
                localStorage.setItem('pestRecords', JSON.stringify(records));
            } catch (e) {
                console.error('Error saving to localStorage:', e);
            }
            showSection('record-section');
        }

        function deleteRecord(id) {
            if (confirm('هل أنت متأكد من الحذف؟')) {
                records = records.filter(r => r.id !== id);
                try {
                    localStorage.setItem('pestRecords', JSON.stringify(records));
                } catch (e) {
                    console.error('Error saving to localStorage:', e);
                }
                renderRecordsTable();
                if (records.length === 0) document.getElementById('no-records').classList.remove('hidden');
            }
        }

        function searchRecords() {
            const term = document.getElementById('search-input').value.toLowerCase().trim();
            if (!term) return renderRecordsTable();
            const results = records.filter(r =>
                r.pestName.toLowerCase().includes(term) ||
                (r.scientificName && r.scientificName.toLowerCase().includes(term)) ||
                r.affectedCrop.toLowerCase().includes(term) ||
                r.symptoms.toLowerCase().includes(term) ||
                (r.pesticide && r.pesticide.toLowerCase().includes(term)) ||
                (r.notes && r.notes.toLowerCase().includes(term)) ||
                r.recordedBy.toLowerCase().includes(term) ||
                r.location.toLowerCase().includes(term)
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
