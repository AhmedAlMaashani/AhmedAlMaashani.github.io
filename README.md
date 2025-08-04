<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>نظام تسجيل الآفات والأمراض النباتية | Pest & Disease Recording System</title>
    <!-- خط عربي داعم للـ PDF والعرض -->
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
    <style>
        :root {
            --primary-color: #27ae60;
            --secondary-color: #2c3e50;
            --danger-color: #e74c3c;
            --light-color: #f5f5f5;
            --dark-color: #333;
            --white: #fff;
            --border-radius: 8px;
        }

        body {
            font-family: 'Cairo', 'Arial', sans-serif;
            margin: 0;
            padding: 0;
            background-color: var(--light-color);
            color: var(--dark-color);
            line-height: 1.8;
            transition: all 0.3s ease;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 15px;
        }

        header {
            background-color: var(--secondary-color);
            color: var(--white);
            padding: 15px 0;
            border-radius: var(--border-radius) var(--border-radius) 0 0;
            margin-bottom: 20px;
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
            margin: 0;
            font-size: 1.4rem;
            font-weight: 600;
        }

        .lang-switcher {
            display: flex;
            gap: 10px;
        }

        .lang-btn {
            padding: 8px 16px;
            background-color: var(--primary-color);
            color: var(--white);
            border: none;
            border-radius: 6px;
            cursor: pointer;
            font-size: 0.95rem;
            font-weight: 600;
            transition: background 0.3s;
        }

        .lang-btn:hover {
            background-color: #229b54;
        }

        .main-menu {
            display: flex;
            gap: 15px;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }

        .menu-btn {
            padding: 12px 20px;
            background-color: var(--secondary-color);
            color: var(--white);
            border: none;
            border-radius: 6px;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            font-size: 1.05rem;
            font-weight: 600;
            flex: 1;
            min-width: 150px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }

        .menu-btn:hover {
            background-color: var(--primary-color);
            transform: translateY(-2px);
        }

        .card {
            background-color: var(--white);
            border-radius: var(--border-radius);
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
            padding: 20px;
            margin-bottom: 20px;
        }

        label {
            display: block;
            margin-bottom: 6px;
            font-weight: 600;
            color: var(--secondary-color);
        }

        input[type="text"],
        input[type="date"],
        textarea,
        select {
            width: 100%;
            padding: 12px;
            border: 1px solid #ddd;
            border-radius: 6px;
            box-sizing: border-box;
            font-size: 1rem;
            font-family: 'Cairo', Arial, sans-serif;
        }

        textarea {
            height: 120px;
            resize: vertical;
        }

        .form-row {
            display: flex;
            gap: 15px;
            margin-bottom: 15px;
        }

        .form-row .form-group {
            flex: 1;
        }

        .camera-section {
            margin: 25px 0;
            text-align: center;
        }

        #camera-preview {
            width: 100%;
            max-width: 400px;
            height: auto;
            max-height: 300px;
            background-color: #eee;
            border: 1px solid #ddd;
            border-radius: 6px;
            margin: 10px auto;
            display: block;
        }

        #capture-btn {
            padding: 12px 24px;
            background-color: var(--primary-color);
            color: var(--white);
            border: none;
            border-radius: 6px;
            cursor: pointer;
            font-size: 1.05rem;
            font-weight: 600;
            display: inline-flex;
            align-items: center;
            gap: 8px;
            margin-top: 10px;
            box-shadow: 0 3px 8px rgba(0,0,0,0.15);
        }

        #capture-btn:hover {
            background-color: #229b54;
        }

        #captured-images {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            margin-top: 15px;
            justify-content: center;
        }

        .image-container {
            position: relative;
            width: 120px;
            height: 120px;
            border-radius: 8px;
            overflow: hidden;
        }

        .image-container img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        .delete-image {
            position: absolute;
            top: 6px;
            right: 6px;
            background-color: var(--danger-color);
            color: var(--white);
            border: none;
            border-radius: 50%;
            width: 28px;
            height: 28px;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            font-size: 0.8rem;
            box-shadow: 0 2px 5px rgba(0,0,0,0.2);
        }

        #submit-btn {
            padding: 14px 32px;
            background-color: var(--primary-color);
            color: var(--white);
            border: none;
            border-radius: 6px;
            cursor: pointer;
            font-size: 1.1rem;
            font-weight: 600;
            display: block;
            margin: 25px auto;
            box-shadow: 0 4px 10px rgba(0,0,0,0.15);
            width: auto;
        }

        #submit-btn:hover {
            background-color: #229b54;
        }

        .records-table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
            font-size: 0.95rem;
        }

        .records-table th, .records-table td {
            padding: 14px 12px;
            text-align: right;
            border-bottom: 1px solid #eee;
        }

        .records-table th {
            background-color: var(--secondary-color);
            color: var(--white);
            font-weight: 600;
        }

        .records-table tr:hover {
            background-color: #f8f9fa;
        }

        .action-btn {
            padding: 8px 12px;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            margin: 0 3px;
            display: inline-flex;
            align-items: center;
            gap: 6px;
            font-size: 0.9rem;
            font-weight: 600;
        }

        .edit-btn {
            background-color: #3498db;
            color: var(--white);
        }

        .delete-btn {
            background-color: var(--danger-color);
            color: var(--white);
        }

        .pdf-btn {
            background-color: #e74c3c;
            color: var(--white);
        }

        .pagination {
            display: flex;
            justify-content: center;
            margin-top: 25px;
            gap: 8px;
            flex-wrap: wrap;
        }

        .page-btn {
            padding: 10px 16px;
            background-color: var(--secondary-color);
            color: var(--white);
            border: none;
            border-radius: 6px;
            cursor: pointer;
            font-size: 0.95rem;
            min-width: 40px;
        }

        .page-btn.active {
            background-color: var(--primary-color);
            transform: scale(1.05);
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
            padding: 12px;
            border: 1px solid #ddd;
            border-radius: 6px;
            font-size: 1rem;
        }

        .search-btn {
            padding: 12px 20px;
            background-color: var(--secondary-color);
            color: var(--white);
            border: none;
            border-radius: 6px;
            cursor: pointer;
            font-weight: 600;
        }

        .no-records {
            text-align: center;
            padding: 30px 20px;
            color: #777;
            font-size: 1.1rem;
        }

        .detail-row {
            display: flex;
            margin-bottom: 12px;
            padding-bottom: 4px;
            border-bottom: 1px dashed #eee;
        }

        .detail-label {
            font-weight: 700;
            width: 160px;
            color: var(--secondary-color);
            flex-shrink: 0;
        }

        .detail-value {
            flex: 1;
            word-wrap: break-word;
        }

        .detail-images {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            margin-top: 20px;
            justify-content: center;
        }

        .detail-image {
            width: 180px;
            height: 180px;
            object-fit: cover;
            border-radius: 8px;
            box-shadow: 0 3px 10px rgba(0,0,0,0.15);
        }

        .back-btn {
            padding: 10px 20px;
            background-color: #7f8c8d;
            color: var(--white);
            border: none;
            border-radius: 6px;
            cursor: pointer;
            margin-bottom: 20px;
            display: inline-flex;
            align-items: center;
            gap: 8px;
            font-weight: 600;
        }

        .hidden {
            display: none !important;
        }

        /* --- تحسينات للهاتف المحمول --- */
        @media (max-width: 768px) {
            .form-row {
                flex-direction: column;
            }
            .header-content {
                text-align: center;
            }
            .menu-btn {
                font-size: 1rem;
                padding: 12px 16px;
                min-width: 120px;
            }
            .records-table th, .records-table td {
                padding: 10px 8px;
                font-size: 0.9rem;
            }
            .action-btn {
                padding: 6px 8px;
                font-size: 0.85rem;
                gap: 4px;
            }
            .detail-row {
                flex-direction: column;
            }
            .detail-label {
                width: 100%;
                margin-bottom: 4px;
            }
            .image-container, .detail-image {
                width: 140px;
                height: 140px;
            }
            #camera-preview {
                max-width: 100%;
            }
        }

        @media (max-width: 480px) {
            .container {
                padding: 10px;
            }
            .card {
                padding: 16px;
            }
            h1 {
                font-size: 1.3rem;
            }
            .menu-btn {
                font-size: 0.95rem;
                padding: 10px 14px;
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
            <button class="menu-btn" onclick="showSection('record-section')" id="record-btn">
                <i class="fas fa-plus-circle"></i>
                <span lang="ar">تسجيل إصابة جديدة</span>
                <span lang="en" class="hidden">New Record</span>
            </button>
            <button class="menu-btn" onclick="showSection('records-section')" id="records-btn">
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
                        <input type="text" id="pest-name" required>
                    </div>
                    <div class="form-group">
                        <label lang="ar">الاسم العلمي</label>
                        <label lang="en" class="hidden">Scientific Name</label>
                        <input type="text" id="scientific-name">
                    </div>
                </div>
                <div class="form-group">
                    <label lang="ar">المحصول المصاب</label>
                    <label lang="en" class="hidden">Affected Crop</label>
                    <input type="text" id="affected-crop" required>
                </div>
                <div class="form-group">
                    <label lang="ar">أعراض الإصابة</label>
                    <label lang="en" class="hidden">Symptoms</label>
                    <textarea id="symptoms" placeholder="صف الأعراض بدقة..." required></textarea>
                </div>
                <div class="camera-section">
                    <h3 lang="ar">تصوير الإصابة</h3>
                    <h3 lang="en" class="hidden">Capture Images</h3>
                    <video id="camera-preview" autoplay playsinline></video>
                    <button type="button" id="capture-btn" onclick="captureImage()">
                        <i class="fas fa-camera"></i>
                        <span lang="ar">التقاط صورة</span>
                        <span lang="en" class="hidden">Capture Image</span>
                    </button>
                    <div id="captured-images"></div>
                </div>
                <div class="form-group">
                    <label lang="ar">المكافحة الكيميائية (اسم المبيد)</label>
                    <label lang="en" class="hidden">Chemical Control (Pesticide Name)</label>
                    <input type="text" id="pesticide">
                </div>
                <div class="form-group">
                    <label lang="ar">ملاحظات إضافية</label>
                    <label lang="en" class="hidden">Additional Notes</label>
                    <textarea id="notes" placeholder="ملاحظات إضافية..."></textarea>
                </div>
                <button type="submit" id="submit-btn">
                    <i class="fas fa-save"></i>
                    <span lang="ar">حفظ البيانات</span>
                    <span lang="en" class="hidden">Save Record</span>
                </button>
            </form>
        </div>

        <!-- قائمة الإصابات -->
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
                            <th lang="ar">الإجراءات</th>
                            <th lang="en" class="hidden">Actions</th>
                        </tr>
                    </thead>
                    <tbody id="records-table-body"></tbody>
                </table>
            </div>
            <div class="no-records hidden" id="no-records">
                <p lang="ar">لا توجد سجلات مسجلة</p>
                <p lang="en" class="hidden">No records found</p>
            </div>
            <div class="pagination" id="pagination"></div>
        </div>

        <!-- تفاصيل الإصابة -->
        <div class="card hidden" id="record-details-section">
            <button class="back-btn" onclick="showSection('records-section')">
                <i class="fas fa-arrow-left"></i>
                <span lang="ar">العودة للقائمة</span>
                <span lang="en" class="hidden">Back to List</span>
            </button>
            <h2 lang="ar">تفاصيل الإصابة</h2>
            <h2 lang="en" class="hidden">Record Details</h2>
            <div class="record-details" id="record-details"></div>
        </div>
    </div>

    <script>
        let currentLanguage = 'ar';
        let records = JSON.parse(localStorage.getItem('pestRecords')) || [];
        let currentPage = 1;
        const recordsPerPage = 5;
        let stream = null;
        let currentRecordId = null;

        document.addEventListener('DOMContentLoaded', function() {
            const today = new Date().toISOString().split('T')[0];
            document.getElementById('discovery-date').value = today;

            initCamera();
            showSection('record-section');
            if (records.length > 0) {
                renderRecordsTable();
            } else {
                document.getElementById('no-records').classList.remove('hidden');
            }
            window.jsPDF = window.jspdf.jsPDF;
        });

        function switchLanguage(lang) {
            currentLanguage = lang;
            document.querySelectorAll('[lang]').forEach(el => {
                if (el.tagName !== 'HTML') el.classList.add('hidden');
            });
            document.querySelectorAll(`[lang="${lang}"]`).forEach(el => {
                el.classList.remove('hidden');
            });
            document.documentElement.lang = lang;
            document.documentElement.dir = lang === 'ar' ? 'rtl' : 'ltr';
            document.body.style.fontFamily = lang === 'ar' ? "'Cairo', Arial, sans-serif" : "Arial, sans-serif";

            if (!document.getElementById('records-section').classList.contains('hidden')) {
                renderRecordsTable();
            }
        }

        function showSection(sectionId) {
            document.querySelectorAll('.card').forEach(section => {
                section.classList.add('hidden');
            });
            document.getElementById(sectionId).classList.remove('hidden');
            if (sectionId === 'records-section') renderRecordsTable();
        }

        async function initCamera() {
            try {
                stream = await navigator.mediaDevices.getUserMedia({ video: { facingMode: 'environment' } });
                document.getElementById('camera-preview').srcObject = stream;
            } catch (err) {
                console.error("Camera access error:", err);
                alert(currentLanguage === 'ar' ? "الكاميرا غير متاحة. تأكد من الأذونات." : "Camera not available. Please check permissions.");
            }
        }

        function captureImage() {
            const video = document.getElementById('camera-preview');
            const canvas = document.createElement('canvas');
            canvas.width = 640;
            canvas.height = 480;
            const ctx = canvas.getContext('2d');
            ctx.drawImage(video, 0, 0, canvas.width, canvas.height);
            const imgData = canvas.toDataURL('image/jpeg', 0.9); // جودة عالية
            addCapturedImage(imgData);
        }

        function addCapturedImage(imgData) {
            const container = document.createElement('div');
            container.className = 'image-container';
            const img = document.createElement('img');
            img.src = imgData;
            const deleteBtn = document.createElement('button');
            deleteBtn.className = 'delete-image';
            deleteBtn.innerHTML = '<i class="fas fa-times"></i>';
            deleteBtn.onclick = () => container.remove();
            container.appendChild(img);
            container.appendChild(deleteBtn);
            document.getElementById('captured-images').appendChild(container);
        }

        document.getElementById('pestForm').addEventListener('submit', function(e) {
            e.preventDefault();
            const formData = {
                id: Date.now().toString(),
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

            records.unshift(formData);
            localStorage.setItem('pestRecords', JSON.stringify(records));
            alert(currentLanguage === 'ar' ? 'تم حفظ السجل بنجاح!' : 'Record saved successfully!');
            this.reset();
            document.getElementById('captured-images').innerHTML = '';
            document.getElementById('discovery-date').value = new Date().toISOString().split('T')[0];
            showSection('records-section');
        });

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
                row.innerHTML = `
                    <td>${record.date}</td>
                    <td>${record.pestName}</td>
                    <td>${record.affectedCrop}</td>
                    <td>
                        <button class="action-btn" onclick="viewRecordDetails('${record.id}')"><i class="fas fa-eye"></i></button>
                        <button class="action-btn edit-btn" onclick="editRecord('${record.id}')"><i class="fas fa-edit"></i></button>
                        <button class="action-btn delete-btn" onclick="deleteRecord('${record.id}')"><i class="fas fa-trash"></i></button>
                        <button class="action-btn pdf-btn" onclick="generatePDF('${record.id}')"><i class="fas fa-file-pdf"></i></button>
                    </td>
                `;
                tableBody.appendChild(row);
            });
            renderPagination();
        }

        function renderPagination() {
            const totalPages = Math.ceil(records.length / recordsPerPage);
            const paginationDiv = document.getElementById('pagination');
            paginationDiv.innerHTML = '';
            if (totalPages <= 1) return;
            for (let i = 1; i <= totalPages; i++) {
                const btn = document.createElement('button');
                btn.className = `page-btn ${i === currentPage ? 'active' : ''}`;
                btn.textContent = i;
                btn.onclick = () => renderRecordsTable(i);
                paginationDiv.appendChild(btn);
            }
        }

        function viewRecordDetails(recordId) {
            const record = records.find(r => r.id === recordId);
            if (!record) return;
            const detailsDiv = document.getElementById('record-details');
            detailsDiv.innerHTML = `
                <div class="detail-row"><div class="detail-label" lang="ar">تاريخ الاكتشاف:</div><div class="detail-value">${record.date}</div></div>
                <div class="detail-row"><div class="detail-label" lang="ar">اسم الإصابة:</div><div class="detail-value">${record.pestName}</div></div>
                <div class="detail-row"><div class="detail-label" lang="ar">الاسم العلمي:</div><div class="detail-value">${record.scientificName || '—'}</div></div>
                <div class="detail-row"><div class="detail-label" lang="ar">المحصول:</div><div class="detail-value">${record.affectedCrop}</div></div>
                <div class="detail-row"><div class="detail-label" lang="ar">الأعراض:</div><div class="detail-value">${record.symptoms}</div></div>
                <div class="detail-row"><div class="detail-label" lang="ar">المبيد:</div><div class="detail-value">${record.pesticide || '—'}</div></div>
                <div class="detail-row"><div class="detail-label" lang="ar">ملاحظات:</div><div class="detail-value">${record.notes || '—'}</div></div>
                <h3 lang="ar">صور الإصابة:</h3>
                <div class="detail-images">${record.images?.length ? record.images.map(src => `<img src="${src}" class="detail-image">`).join('') : (currentLanguage === 'ar' ? 'لا توجد صور' : 'No images')}</div>
            `;
            switchLanguage(currentLanguage); // تأكد من تحديث اللغة
            showSection('record-details-section');
        }

        function generatePDF(recordId) {
            const record = records.find(r => r.id === recordId);
            if (!record) return;

            const { jsPDF } = window.jspdf;
            const doc = new jsPDF({
                orientation: 'portrait',
                unit: 'mm',
                format: 'a4'
            });

            // تضمين الخط العربي (مهم للعرض الصحيح)
            doc.setFont('Cairo');

            // العنوان
            doc.setFontSize(20);
            doc.setTextColor(40, 40, 40);
            doc.text(currentLanguage === 'ar' ? 'تقرير الإصابة النباتية' : 'Plant Pest/Disease Report', 105, 20, { align: 'center' });

            // البيانات
            doc.setFontSize(14);
            let y = 40;
            const leftMargin = 20;
            const maxWidth = 170;

            doc.text(`${currentLanguage === 'ar' ? 'تاريخ الاكتشاف:' : 'Discovery Date:'} ${record.date}`, leftMargin, y); y += 15;
            doc.text(`${currentLanguage === 'ar' ? 'اسم الإصابة:' : 'Pest/Disease Name:'} ${record.pestName}`, leftMargin, y); y += 15;
            if (record.scientificName) {
                doc.text(`${currentLanguage === 'ar' ? 'الاسم العلمي:' : 'Scientific Name:'} ${record.scientificName}`, leftMargin, y); y += 15;
            }
            doc.text(`${currentLanguage === 'ar' ? 'المحصول:' : 'Crop:'} ${record.affectedCrop}`, leftMargin, y); y += 15;

            // الأعراض
            doc.text(`${currentLanguage === 'ar' ? 'أعراض الإصابة:' : 'Symptoms:'}`, leftMargin, y);
            y += 8;
            const symptomsLines = doc.splitTextToSize(record.symptoms, maxWidth);
            doc.text(symptomsLines, leftMargin, y);
            y += symptomsLines.length * 6 + 10;

            if (record.pesticide) {
                doc.text(`${currentLanguage === 'ar' ? 'المبيد المستخدم:' : 'Pesticide Used:'} ${record.pesticide}`, leftMargin, y); y += 15;
            }
            if (record.notes) {
                doc.text(`${currentLanguage === 'ar' ? 'ملاحظات:' : 'Notes:'}`, leftMargin, y); y += 8;
                const notesLines = doc.splitTextToSize(record.notes, maxWidth);
                doc.text(notesLines, leftMargin, y); y += notesLines.length * 6 + 10;
            }

            // الصور
            if (record.images && record.images.length > 0) {
                doc.addPage();
                doc.text(`${currentLanguage === 'ar' ? 'صور الإصابة' : 'Pest Images'}`, leftMargin, 20);
                y = 30;

                record.images.forEach((img, index) => {
                    if (index > 0 && index % 2 === 0) {
                        doc.addPage();
                        y = 30;
                    }
                    if (index % 2 === 1) y = 120;

                    doc.addImage(img, 'JPEG', 20, y, 80, 80);
                    if (index % 2 === 0 && index < record.images.length - 1) {
                        // صورة ثانية في نفس الصفحة
                        doc.addImage(record.images[index + 1], 'JPEG', 110, y, 80, 80);
                    }
                    y += 90;
                });
            }

            doc.save(`${record.pestName}_${record.date}.pdf`);
        }

        function editRecord(recordId) {
            const record = records.find(r => r.id === recordId);
            if (!record) return;
            Object.assign(document, {
                'discovery-date': record.date,
                'pest-name': record.pestName,
                'scientific-name': record.scientificName || '',
                'affected-crop': record.affectedCrop,
                'symptoms': record.symptoms,
                'pesticide': record.pesticide || '',
                'notes': record.notes || ''
            });
            document.getElementById('discovery-date').value = record.date;
            document.getElementById('pest-name').value = record.pestName;
            document.getElementById('scientific-name').value = record.scientificName || '';
            document.getElementById('affected-crop').value = record.affectedCrop;
            document.getElementById('symptoms').value = record.symptoms;
            document.getElementById('pesticide').value = record.pesticide || '';
            document.getElementById('notes').value = record.notes || '';

            const imagesContainer = document.getElementById('captured-images');
            imagesContainer.innerHTML = '';
            (record.images || []).forEach(imgData => addCapturedImage(imgData));

            records = records.filter(r => r.id !== recordId);
            localStorage.setItem('pestRecords', JSON.stringify(records));
            showSection('record-section');
        }

        function deleteRecord(recordId) {
            if (confirm(currentLanguage === 'ar' ? 'هل أنت متأكد من الحذف؟' : 'Are you sure you want to delete this record?')) {
                records = records.filter(r => r.id !== recordId);
                localStorage.setItem('pestRecords', JSON.stringify(records));
                renderRecordsTable();
                if (records.length === 0) document.getElementById('no-records').classList.remove('hidden');
            }
        }

        function searchRecords() {
            const input = currentLanguage === 'ar' ? document.getElementById('search-input') : document.getElementById('search-input-en');
            const term = input.value.toLowerCase().trim();
            if (!term) return renderRecordsTable();

            const filtered = records.filter(r =>
                r.pestName.toLowerCase().includes(term) ||
                (r.scientificName && r.scientificName.toLowerCase().includes(term)) ||
                r.affectedCrop.toLowerCase().includes(term) ||
                r.symptoms.toLowerCase().includes(term) ||
                (r.pesticide && r.pesticide.toLowerCase().includes(term)) ||
                (r.notes && r.notes.toLowerCase().includes(term))
            );
            renderSearchResults(filtered);
        }

        function renderSearchResults(results) {
            const tbody = document.getElementById('records-table-body');
            tbody.innerHTML = results.length ? results.map(r => `
                <tr>
                    <td>${r.date}</td>
                    <td>${r.pestName}</td>
                    <td>${r.affectedCrop}</td>
                    <td>
                        <button class="action-btn" onclick="viewRecordDetails('${r.id}')"><i class="fas fa-eye"></i></button>
                        <button class="action-btn edit-btn" onclick="editRecord('${r.id}')"><i class="fas fa-edit"></i></button>
                        <button class="action-btn delete-btn" onclick="deleteRecord('${r.id}')"><i class="fas fa-trash"></i></button>
                        <button class="action-btn pdf-btn" onclick="generatePDF('${r.id}')"><i class="fas fa-file-pdf"></i></button>
                    </td>
                </tr>
            `).join('') : '';
            document.getElementById('no-records').classList.toggle('hidden', results.length > 0);
            document.getElementById('pagination').innerHTML = '';
        }
    </script>
</body>
</html>
