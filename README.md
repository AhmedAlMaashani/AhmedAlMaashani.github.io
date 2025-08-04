<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>نظام تسجيل الآفات والأمراض النباتية | Pest & Disease Recording System</title>
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
        }
        body {
            font-family: 'Arial', sans-serif;
            margin: 0;
            padding: 0;
            background-color: var(--light-color);
            transition: all 0.3s ease;
        }
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }
        header {
            background-color: var(--secondary-color);
            color: var(--white);
            padding: 15px 0;
            border-radius: 8px 8px 0 0;
            margin-bottom: 20px;
        }
        .header-content {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 0 20px;
        }
        h1 {
            margin: 0;
            font-size: 1.5rem;
        }
        .lang-switcher {
            display: flex;
            gap: 10px;
        }
        .lang-btn {
            padding: 5px 15px;
            background-color: var(--primary-color);
            color: var(--white);
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 0.9rem;
        }
        .main-menu {
            display: flex;
            gap: 15px;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }
        .menu-btn {
            padding: 10px 20px;
            background-color: var(--secondary-color);
            color: var(--white);
            border: none;
            border-radius: 4px;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 8px;
            font-size: 1rem;
        }
        .menu-btn i {
            font-size: 1.1rem;
        }
        .menu-btn:hover {
            background-color: var(--primary-color);
        }
        .card {
            background-color: var(--white);
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
            padding: 20px;
            margin-bottom: 20px;
        }
        .form-group {
            margin-bottom: 15px;
        }
        label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
            color: var(--secondary-color);
        }
        input[type="text"],
        input[type="date"],
        textarea,
        select {
            width: 100%;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 4px;
            box-sizing: border-box;
            font-size: 1rem;
        }
        textarea {
            height: 100px;
            resize: vertical;
        }
        .camera-section {
            margin: 20px 0;
            text-align: center;
        }
        #camera-preview {
            width: 100%;
            max-width: 500px;
            background-color: #eee;
            margin-bottom: 10px;
            border-radius: 4px;
        }
        #capture-btn {
            padding: 10px 20px;
            background-color: var(--primary-color);
            color: var(--white);
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 1rem;
            display: inline-flex;
            align-items: center;
            gap: 8px;
        }
        #submit-btn {
            padding: 12px 30px;
            background-color: var(--primary-color);
            color: var(--white);
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 1.1rem;
            display: block;
            margin: 20px auto;
        }
        .hidden {
            display: none;
        }
        .form-row {
            display: flex;
            gap: 15px;
        }
        .form-row .form-group {
            flex: 1;
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
            width: 150px;
            height: 150px;
        }
        .image-container img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            border-radius: 4px;
        }
        .delete-image {
            position: absolute;
            top: 5px;
            right: 5px;
            background-color: var(--danger-color);
            color: var(--white);
            border: none;
            border-radius: 50%;
            width: 25px;
            height: 25px;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
        }
        .records-table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }
        .records-table th, .records-table td {
            padding: 12px 15px;
            text-align: right;
            border-bottom: 1px solid #ddd;
        }
        .records-table th {
            background-color: var(--secondary-color);
            color: var(--white);
        }
        .records-table tr:hover {
            background-color: #f9f9f9;
        }
        .action-btn {
            padding: 5px 10px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            margin-left: 5px;
            display: inline-flex;
            align-items: center;
            gap: 5px;
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
            margin-top: 20px;
            gap: 5px;
        }
        .page-btn {
            padding: 8px 12px;
            background-color: var(--secondary-color);
            color: var(--white);
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
        .page-btn.active {
            background-color: var(--primary-color);
        }
        .search-container {
            margin-bottom: 20px;
            display: flex;
            gap: 10px;
        }
        .search-input {
            flex: 1;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 4px;
        }
        .search-btn {
            padding: 10px 20px;
            background-color: var(--secondary-color);
            color: var(--white);
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
        .no-records {
            text-align: center;
            padding: 20px;
            color: #777;
        }
        .record-details {
            margin-top: 20px;
        }
        .detail-row {
            display: flex;
            margin-bottom: 10px;
        }
        .detail-label {
            font-weight: bold;
            width: 150px;
            color: var(--secondary-color);
        }
        .detail-value {
            flex: 1;
        }
        .detail-images {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            margin-top: 20px;
        }
        .detail-image {
            width: 200px;
            height: 200px;
            object-fit: cover;
            border-radius: 4px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        .back-btn {
            padding: 10px 20px;
            background-color: #7f8c8d;
            color: var(--white);
            border: none;
            border-radius: 4px;
            cursor: pointer;
            margin-bottom: 20px;
            display: inline-flex;
            align-items: center;
            gap: 8px;
        }
        @media (max-width: 768px) {
            .form-row {
                flex-direction: column;
            }
            .header-content {
                flex-direction: column;
                gap: 15px;
                text-align: center;
            }
            .records-table th, .records-table td {
                padding: 8px;
                font-size: 0.9rem;
            }
            .action-btn {
                padding: 3px 6px;
                font-size: 0.8rem;
            }
            .detail-row {
                flex-direction: column;
            }
            .detail-label {
                width: 100%;
                margin-bottom: 5px;
            }
        }
        @media (max-width: 480px) {
            .menu-btn {
                padding: 8px 15px;
                font-size: 0.9rem;
            }
            .search-container {
                flex-direction: column;
            }
            .image-container {
                width: 120px;
                height: 120px;
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
                    <textarea id="symptoms" required></textarea>
                </div>
                <div class="camera-section">
                    <h3 lang="ar">تصوير الإصابة</h3>
                    <h3 lang="en" class="hidden">Capture Images</h3>
                    <video id="camera-preview" autoplay></video>
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
                    <textarea id="notes"></textarea>
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
                <input type="text" class="search-input" id="search-input" placeholder="ابحث..." lang="ar">
                <input type="text" class="search-input hidden" id="search-input-en" placeholder="Search..." lang="en">
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
                    <tbody id="records-table-body">
                        <!-- سيتم ملؤها بالبيانات من localStorage -->
                    </tbody>
                </table>
            </div>
            <div class="no-records hidden" id="no-records">
                <p lang="ar">لا توجد سجلات مسجلة</p>
                <p lang="en" class="hidden">No records found</p>
            </div>
            <div class="pagination" id="pagination">
                <!-- سيتم ملؤها بالترقيم -->
            </div>
        </div>
        <!-- تفاصيل الإصابة -->
        <div class="card hidden" id="record-details-section">
            <button class="back-btn" onclick="showSection('records-section')">
                <i class="fas fa-arrow-left"></i>
                <span lang="ar">العودة للقائمة</span>
                <span lang="en" class="hidden">Back to List</span>
            </button>
            <h2 id="detail-title" lang="ar">تفاصيل الإصابة</h2>
            <h2 id="detail-title-en" lang="en" class="hidden">Record Details</h2>
            <div class="record-details" id="record-details">
                <!-- سيتم ملؤها بالتفاصيل -->
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
            
            // تهيئة الكاميرا
            initCamera();
            
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
        }
        
        // عرض قسم معين وإخفاء الأقسام الأخرى
        function showSection(sectionId) {
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
        }
        
        // تهيئة الكاميرا
        async function initCamera() {
            try {
                stream = await navigator.mediaDevices.getUserMedia({ video: true });
                document.getElementById('camera-preview').srcObject = stream;
            } catch (err) {
                console.error("Error accessing camera:", err);
                alert(currentLanguage === 'ar' ? "تعذر الوصول إلى الكاميرا. يرجى التحقق من الأذونات." : "Could not access camera. Please check permissions.");
            }
        }
        
        // التقاط صورة
        function captureImage() {
            const video = document.getElementById('camera-preview');
            const canvas = document.createElement('canvas');
            canvas.width = video.videoWidth;
            canvas.height = video.videoHeight;
            const ctx = canvas.getContext('2d');
            ctx.drawImage(video, 0, 0, canvas.width, canvas.height);
            const imgData = canvas.toDataURL('image/jpeg');
            addCapturedImage(imgData);
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
            // عرض رسالة نجاح
            alert(currentLanguage === 'ar' ? 'تم حفظ السجل بنجاح!' : 'Record saved successfully!');
            // إعادة تعيين النموذج
            this.reset();
            document.getElementById('captured-images').innerHTML = '';
            document.getElementById('discovery-date').value = new Date().toISOString().split('T')[0];
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
                // الإجراءات
                const actionsCell = document.createElement('td');
                // زر التفاصيل
                const viewBtn = document.createElement('button');
                viewBtn.className = 'action-btn';
                viewBtn.innerHTML = '<i class="fas fa-eye"></i>';
                viewBtn.title = currentLanguage === 'ar' ? 'عرض التفاصيل' : 'View Details';
                viewBtn.onclick = () => viewRecordDetails(record.id);
                actionsCell.appendChild(viewBtn);
                // زر التعديل
                const editBtn = document.createElement('button');
                editBtn.className = 'action-btn edit-btn';
                editBtn.innerHTML = '<i class="fas fa-edit"></i>';
                editBtn.title = currentLanguage === 'ar' ? 'تعديل' : 'Edit';
                editBtn.onclick = () => editRecord(record.id);
                actionsCell.appendChild(editBtn);
                // زر الحذف
                const deleteBtn = document.createElement('button');
                deleteBtn.className = 'action-btn delete-btn';
                deleteBtn.innerHTML = '<i class="fas fa-trash"></i>';
                deleteBtn.title = currentLanguage === 'ar' ? 'حذف' : 'Delete';
                deleteBtn.onclick = () => deleteRecord(record.id);
                actionsCell.appendChild(deleteBtn);
                // زر PDF
                const pdfBtn = document.createElement('button');
                pdfBtn.className = 'action-btn pdf-btn';
                pdfBtn.innerHTML = '<i class="fas fa-file-pdf"></i>';
                pdfBtn.title = currentLanguage === 'ar' ? 'تصدير PDF' : 'Export PDF';
                pdfBtn.onclick = () => generatePDF(record.id);
                actionsCell.appendChild(pdfBtn);
                row.appendChild(actionsCell);
                tableBody.appendChild(row);
            });
            // إنشاء الترقيم
            renderPagination();
        }
        
        // إنشاء الترقيم
        function renderPagination() {
            const totalPages = Math.ceil(records.length / recordsPerPage);
            const paginationDiv = document.getElementById('pagination');
            paginationDiv.innerHTML = '';
            if (totalPages <= 1) return;
            for (let i = 1; i <= totalPages; i++) {
                const pageBtn = document.createElement('button');
                pageBtn.className = 'page-btn' + (i === currentPage ? ' active' : '');
                pageBtn.textContent = i;
                pageBtn.onclick = () => renderRecordsTable(i);
                paginationDiv.appendChild(pageBtn);
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
                <h3 lang="ar" style="margin-top: 20px;">صور الإصابة:</h3>
                <h3 lang="en" class="hidden" style="margin-top: 20px;">Pest/Disease Images:</h3>
                <div class="detail-images" id="detail-images">
                    ${record.images && record.images.length > 0 ? 
                      record.images.map(img => `<img src="${img}" class="detail-image">`).join('') : 
                      (currentLanguage === 'ar' ? 'لا توجد صور' : 'No images')}
                </div>
            `;
            showSection('record-details-section');
        }
        
        // تعديل السجل
        function editRecord(recordId) {
            const record = records.find(r => r.id === recordId);
            if (!record) return;
            // ملء النموذج ببيانات السجل
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
                // الإجراءات
                const actionsCell = document.createElement('td');
                // زر التفاصيل
                const viewBtn = document.createElement('button');
                viewBtn.className = 'action-btn';
                viewBtn.innerHTML = '<i class="fas fa-eye"></i>';
                viewBtn.title = currentLanguage === 'ar' ? 'عرض التفاصيل' : 'View Details';
                viewBtn.onclick = () => viewRecordDetails(record.id);
                actionsCell.appendChild(viewBtn);
                // زر التعديل
                const editBtn = document.createElement('button');
                editBtn.className = 'action-btn edit-btn';
                editBtn.innerHTML = '<i class="fas fa-edit"></i>';
                editBtn.title = currentLanguage === 'ar' ? 'تعديل' : 'Edit';
                editBtn.onclick = () => editRecord(record.id);
                actionsCell.appendChild(editBtn);
                // زر الحذف
                const deleteBtn = document.createElement('button');
                deleteBtn.className = 'action-btn delete-btn';
                deleteBtn.innerHTML = '<i class="fas fa-trash"></i>';
                deleteBtn.title = currentLanguage === 'ar' ? 'حذف' : 'Delete';
                deleteBtn.onclick = () => deleteRecord(record.id);
                actionsCell.appendChild(deleteBtn);
                // زر PDF
                const pdfBtn = document.createElement('button');
                pdfBtn.className = 'action-btn pdf-btn';
                pdfBtn.innerHTML = '<i class="fas fa-file-pdf"></i>';
                pdfBtn.title = currentLanguage === 'ar' ? 'تصدير PDF' : 'Export PDF';
                pdfBtn.onclick = () => generatePDF(record.id);
                actionsCell.appendChild(pdfBtn);
                row.appendChild(actionsCell);
                tableBody.appendChild(row);
            });
            document.getElementById('pagination').innerHTML = '';
        }
        
        // توليد ملف PDF باستخدام html2canvas
        async function generatePDF(recordId) {
            const record = records.find(r => r.id === recordId);
            if (!record) return;
            
            // إنشاء عنصر مؤقت لتصدير PDF
            const tempDiv = document.createElement('div');
            tempDiv.style.position = 'absolute';
            tempDiv.style.left = '-9999px';
            tempDiv.style.width = '210mm';
            tempDiv.style.padding = '20px';
            tempDiv.style.fontFamily = "'Arial', sans-serif";
            tempDiv.style.direction = 'rtl';
            tempDiv.style.backgroundColor = 'white';
            tempDiv.style.fontSize = '14px';
            tempDiv.style.lineHeight = '1.6';
            
            // بناء محتوى PDF
            tempDiv.innerHTML = `
                <div style="text-align: center; margin-bottom: 20px;">
                    <h1 style="color: #2c3e50; font-size: 24px; margin-bottom: 5px; font-weight: 700;">تقرير الإصابة النباتية</h1>
                    <p style="font-size: 16px; color: #555;">تاريخ التقرير: ${new Date().toLocaleDateString()}</p>
                </div>
                
                <div style="margin-bottom: 20px;">
                    <h3 style="color: #2c3e50; font-size: 18px; border-bottom: 1px solid #eee; padding-bottom: 10px;">معلومات الإصابة</h3>
                    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 15px; margin-top: 15px;">
                        <div><strong style="color: #2c3e50;">تاريخ الاكتشاف:</strong> ${record.date}</div>
                        <div><strong style="color: #2c3e50;">اسم الإصابة:</strong> ${record.pestName}</div>
                        <div><strong style="color: #2c3e50;">الاسم العلمي:</strong> ${record.scientificName || '-'}</div>
                        <div><strong style="color: #2c3e50;">المحصول المصاب:</strong> ${record.affectedCrop}</div>
                        <div style="grid-column: 1 / 3;"><strong style="color: #2c3e50;">أعراض الإصابة:</strong> ${record.symptoms}</div>
                        <div><strong style="color: #2c3e50;">المكافحة الكيميائية:</strong> ${record.pesticide || '-'}</div>
                        <div><strong style="color: #2c3e50;">ملاحظات إضافية:</strong> ${record.notes || '-'}</div>
                    </div>
                </div>
                
                ${record.images && record.images.length > 0 ? `
                <div style="margin-bottom: 20px;">
                    <h3 style="color: #2c3e50; font-size: 18px; border-bottom: 1px solid #eee; padding-bottom: 10px;">صور الإصابة</h3>
                    <div style="display: flex; flex-wrap: wrap; gap: 15px; margin-top: 15px;">
                        ${record.images.map(img => `
                        <div style="flex: 1; min-width: 200px; max-width: 300px;">
                            <img src="${img}" style="width: 100%; height: auto; border-radius: 8px; box-shadow: 0 2px 10px rgba(0,0,0,0.1);">
                        </div>
                        `).join('')}
                    </div>
                </div>
                ` : ''}
                
                <div style="text-align: center; margin-top: 30px; font-size: 12px; color: #777; border-top: 1px solid #eee; padding-top: 15px;">
                    تم إنشاء هذا التقرير باستخدام نظام تسجيل الآفات والأمراض النباتية
                </div>
            `;
            
            document.body.appendChild(tempDiv);
            
            try {
                // تحويل HTML إلى صورة باستخدام html2canvas
                const canvas = await html2canvas(tempDiv, {
                    scale: 2,
                    useCORS: true,
                    allowTaint: true,
                    logging: false,
                    backgroundColor: 'white'
                });
                
                // إنشاء PDF من الصورة
                const pdf = new jsPDF({
                    orientation: 'portrait',
                    unit: 'mm',
                    format: 'a4'
                });
                
                const imgData = canvas.toDataURL('image/jpeg', 0.95);
                const pdfWidth = pdf.internal.pageSize.getWidth();
                const pdfHeight = (canvas.height * pdfWidth) / canvas.width;
                
                pdf.addImage(imgData, 'JPEG', 0, 0, pdfWidth, pdfHeight);
                pdf.save(`${record.pestName}_${record.date}.pdf`);
                
            } catch (error) {
                console.error('حدث خطأ أثناء إنشاء PDF:', error);
                alert(currentLanguage === 'ar' ? 'حدث خطأ أثناء إنشاء الملف. يرجى المحاولة مرة أخرى.' : 'Error generating PDF. Please try again.');
            } finally {
                document.body.removeChild(tempDiv);
            }
        }
    </script>
</body>
</html>
