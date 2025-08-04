<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>نظام تسجيل الآفات والأمراض النباتية</title>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600&display=swap" rel="stylesheet">
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
        select,
        input[type="file"] {
            width: 100%;
            padding: 12px;
            border: 1px solid #ddd;
            border-radius: 6px;
            box-sizing: border-box;
            font-size: 1rem;
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

        #capture-btn,
        .upload-btn {
            padding: 12px 20px;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            font-size: 1.05rem;
            font-weight: 600;
            display: inline-flex;
            align-items: center;
            gap: 8px;
            margin: 5px;
            box-shadow: 0 3px 8px rgba(0,0,0,0.15);
        }

        #capture-btn {
            background-color: var(--primary-color);
            color: var(--white);
        }

        .upload-btn {
            background-color: #3498db;
            color: var(--white);
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

        .edit-btn { background-color: #3498db; color: var(--white); }
        .delete-btn { background-color: var(--danger-color); color: var(--white); }
        .pdf-btn { background-color: #e74c3c; color: var(--white); }

        .pagination {
            display: flex;
            justify-content: center;
            margin-top: 25px;
            gap: 8px;
        }

        .page-btn {
            padding: 10px 16px;
            background-color: var(--secondary-color);
            color: var(--white);
            border: none;
            border-radius: 6px;
            cursor: pointer;
            font-size: 0.95rem;
        }

        .page-btn.active {
            background-color: var(--primary-color);
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
        }

        .search-btn {
            padding: 12px 20px;
            background-color: var(--secondary-color);
            color: var(--white);
            border: none;
            border-radius: 6px;
            cursor: pointer;
        }

        .no-records {
            text-align: center;
            padding: 30px 20px;
            color: #777;
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

        @media (max-width: 768px) {
            .form-row { flex-direction: column; }
            .menu-btn { font-size: 1rem; padding: 12px 16px; }
            .action-btn { padding: 6px 8px; font-size: 0.85rem; }
            .image-container, .detail-image { width: 140px; height: 140px; }
        }

        @media (max-width: 480px) {
            .container { padding: 10px; }
            .card { padding: 16px; }
            .search-container { flex-direction: column; }
            .search-input, .search-btn { width: 100%; }
            .detail-image { width: 100%; height: auto; }
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
            <form id="pestForm">
                <div class="form-group">
                    <label lang="ar">تاريخ الاكتشاف</label>
                    <input type="date" id="discovery-date" required>
                </div>
                <div class="form-row">
                    <div class="form-group">
                        <label lang="ar">اسم الإصابة المحتملة</label>
                        <input type="text" id="pest-name" required>
                    </div>
                    <div class="form-group">
                        <label lang="ar">الاسم العلمي</label>
                        <input type="text" id="scientific-name">
                    </div>
                </div>
                <div class="form-group">
                    <label lang="ar">المحصول المصاب</label>
                    <input type="text" id="affected-crop" required>
                </div>
                <div class="form-group">
                    <label lang="ar">أعراض الإصابة</label>
                    <textarea id="symptoms" placeholder="صف الأعراض بدقة..." required></textarea>
                </div>

                <div class="camera-section">
                    <h3 lang="ar">إضافة صور للإصابة</h3>
                    <video id="camera-preview" autoplay playsinline></video>
                    <button type="button" id="capture-btn" onclick="captureImage()">
                        <i class="fas fa-camera"></i> التقاط صورة
                    </button>
                    <label for="file-upload" class="upload-btn">
                        <i class="fas fa-upload"></i> اختر من الجهاز
                    </label>
                    <input type="file" id="file-upload" accept="image/*" class="hidden" multiple onchange="handleFileSelect(event)">
                    <div id="captured-images"></div>
                </div>

                <div class="form-group">
                    <label lang="ar">اسم المبيد (إن وُجد)</label>
                    <input type="text" id="pesticide">
                </div>
                <div class="form-group">
                    <label lang="ar">ملاحظات إضافية</label>
                    <textarea id="notes" placeholder="ملاحظات..."></textarea>
                </div>
                <button type="submit" id="submit-btn">
                    <i class="fas fa-save"></i> حفظ السجل
                </button>
            </form>
        </div>

        <!-- قائمة السجلات -->
        <div class="card hidden" id="records-section">
            <h2 lang="ar">قائمة الإصابات</h2>
            <div class="search-container">
                <input type="text" class="search-input" id="search-input" placeholder="ابحث في السجلات...">
                <button class="search-btn" onclick="searchRecords()">
                    <i class="fas fa-search"></i> بحث
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
            <div class="no-records hidden" id="no-records">لا توجد سجلات</div>
            <div class="pagination" id="pagination"></div>
        </div>

        <!-- تفاصيل السجل -->
        <div class="card hidden" id="record-details-section">
            <button class="back-btn" onclick="showSection('records-section')">
                <i class="fas fa-arrow-left"></i> العودة
            </button>
            <h2>تفاصيل السجل</h2>
            <div id="record-details"></div>
        </div>
    </div>

    <script>
        // تضمين خط عربي داعم (Cairo كمثال بصيغة Base64)
        const cairoFont = `data:application/font-woff2;charset=utf-8;base64,d09GMgABAAAAAAZ0ABAAAAAACDQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAGhMgJw8AAwE2AAQAAAAABDgF8wAATYQAAAc4AAAAGAAMADZnbHlm0gAAATwAAAGuAAEC1vTc+D9tYXNwAAABlAAAAdwAAASg4Kc4j2dhc3AAAALcAAAACAAAAAgAAAAQZ2x5Zl7Bw+kAAAHgAAABtQAAAcg1aCQxaGVhZAAAAdAAAAAxAAAANh42f99oaGVhAAAB9AAAACAAAAAkFzQDAGgjb20AAAH8AAABJgAAAUYo+wEAbWF4cAAAAgQAAAAgAAAAIAFMAAFuYW1lAAACFAAAALwAAAHhQ+27h3Bvc3QAAAL8AAAAEgAAACD/9wAveJxjYGRgYOBk8GCcyyDD0MPCAAZGIPQBiTICFQDpPAaG/xD9TAwhAPf0EgR4nGNgZGBg4GB69v8QgwNDFsMdRmMgZWRgYGJgYmQCChgD8T8GIPqH8f97/w245jL9Yz3A9IepEgMAD+4L3XicY2BkYGAA4m0MDiz7GP6z8jHAAJMAo5Ghn+mf6X+mf2b/mf6Z/Gf8z/ifyQ9EMwAAy8wLx3icY2BkYGB99v8QgwNDFsMdRmMgZWRAA4kC2RwMBgD6qQjveJxjYGRgYOBkUH7Az8Dw3+0/IwOjHARzYGBkYGBiYgIKMAYCQBSMZgAAAHcaBIQAAAAAAAB4nGNgZGBg4GRgYQBIAHkAHuACZgAAeJxjYGRgYOBkYGBgZGBgZgABEMnIABJhYGBiAAowAPHzDAgTMy87P4MjiB9RwZjAxMDA/HPp/9V/N/6d+Hf83/F/J/+d+Hf834l/J/+d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+Hfi34l/J/6d+H......`; // (تم تقصير للعرض)

        let currentLanguage = 'ar';
        let records = JSON.parse(localStorage.getItem('pestRecords')) || [];

        document.addEventListener('DOMContentLoaded', () => {
            document.getElementById('discovery-date').value = new Date().toISOString().split('T')[0];
            initCamera();
            showSection('record-section');
            if (records.length > 0) renderRecordsTable();
            else document.getElementById('no-records').classList.remove('hidden');
            window.jsPDF = window.jspdf.jsPDF;
            // إضافة الخط العربي إلى jsPDF
            jsPDF.API.events.push(['addFonts', function() {
                this.addFileToVFS('Cairo-Regular.ttf', cairoFont.split(',')[1]);
                this.addFont('Cairo-Regular.ttf', 'Cairo', 'normal');
            }]);
        });

        function switchLanguage(lang) {
            currentLanguage = lang;
            document.querySelectorAll('[lang]').forEach(el => el.classList.add('hidden'));
            document.querySelectorAll(`[lang="${lang}"]`).forEach(el => el.classList.remove('hidden'));
            document.documentElement.lang = lang;
            document.documentElement.dir = lang === 'ar' ? 'rtl' : 'ltr';
            if (!document.getElementById('records-section').classList.contains('hidden')) renderRecordsTable();
        }

        function showSection(id) {
            document.querySelectorAll('.card').forEach(s => s.classList.add('hidden'));
            document.getElementById(id).classList.remove('hidden');
            if (id === 'records-section') renderRecordsTable();
        }

        async function initCamera() {
            try {
                const stream = await navigator.mediaDevices.getUserMedia({ video: true });
                document.getElementById('camera-preview').srcObject = stream;
            } catch (err) {
                console.warn("Camera not available");
            }
        }

        function captureImage() {
            const video = document.getElementById('camera-preview');
            const canvas = document.createElement('canvas');
            canvas.width = 640;
            canvas.height = 480;
            canvas.getContext('2d').drawImage(video, 0, 0, canvas.width, canvas.height);
            addImageToContainer(canvas.toDataURL('image/jpeg', 0.9));
        }

        function handleFileSelect(e) {
            Array.from(e.target.files).forEach(file => {
                const reader = new FileReader();
                reader.onload = (event) => addImageToContainer(event.target.result);
                reader.readAsDataURL(file);
            });
        }

        function addImageToContainer(src) {
            const div = document.createElement('div');
            div.className = 'image-container';
            div.innerHTML = `
                <img src="${src}" alt="Image">
                <button class="delete-image" onclick="this.parentElement.remove()"><i class="fas fa-times"></i></button>
            `;
            document.getElementById('captured-images').appendChild(div);
        }

        document.getElementById('pestForm').addEventListener('submit', function(e) {
            e.preventDefault();
            const form = this;
            const formData = {
                id: Date.now().toString(),
                date: form.discovery-date.value,
                pestName: form['pest-name'].value,
                scientificName: form['scientific-name'].value,
                affectedCrop: form['affected-crop'].value,
                symptoms: form.symptoms.value,
                pesticide: form.pesticide.value,
                notes: form.notes.value,
                images: Array.from(document.querySelectorAll('#captured-images img')).map(img => img.src),
                createdAt: new Date().toISOString()
            };
            records.unshift(formData);
            localStorage.setItem('pestRecords', JSON.stringify(records));
            alert('تم الحفظ بنجاح!');
            form.reset();
            document.getElementById('captured-images').innerHTML = '';
            document.getElementById('discovery-date').value = new Date().toISOString().split('T')[0];
            showSection('records-section');
        });

        function renderRecordsTable(page = 1) {
            const start = (page - 1) * 5;
            const data = records.slice(start, start + 5);
            const tbody = document.getElementById('records-table-body');
            tbody.innerHTML = data.length ? data.map(r => `
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
            document.getElementById('no-records').classList.toggle('hidden', data.length > 0);
            renderPagination();
        }

        function renderPagination() {
            const pages = Math.ceil(records.length / 5);
            const div = document.getElementById('pagination');
            div.innerHTML = '';
            if (pages <= 1) return;
            for (let i = 1; i <= pages; i++) {
                const btn = document.createElement('button');
                btn.textContent = i;
                btn.className = 'page-btn' + (i === 1 ? ' active' : '');
                btn.onclick = () => renderRecordsTable(i);
                div.appendChild(btn);
            }
        }

        function viewRecord(id) {
            const r = records.find(r => r.id === id);
            if (!r) return;
            document.getElementById('record-details').innerHTML = `
                <div class="detail-row"><div class="detail-label">التاريخ:</div><div class="detail-value">${r.date}</div></div>
                <div class="detail-row"><div class="detail-label">الإصابة:</div><div class="detail-value">${r.pestName}</div></div>
                <div class="detail-row"><div class="detail-label">الاسم العلمي:</div><div class="detail-value">${r.scientificName || '—'}</div></div>
                <div class="detail-row"><div class="detail-label">المحصول:</div><div class="detail-value">${r.affectedCrop}</div></div>
                <div class="detail-row"><div class="detail-label">الأعراض:</div><div class="detail-value">${r.symptoms}</div></div>
                <div class="detail-row"><div class="detail-label">المبيد:</div><div class="detail-value">${r.pesticide || '—'}</div></div>
                <div class="detail-row"><div class="detail-label">ملاحظات:</div><div class="detail-value">${r.notes || '—'}</div></div>
                <h3>الصور:</h3>
                <div class="detail-images">${r.images.map(s => `<img src="${s}" class="detail-image">`).join('') || 'لا توجد صور'}</div>
            `;
            showSection('record-details-section');
        }

        function generatePDF(id) {
            const r = records.find(r => r.id === id);
            if (!r) return;
            const doc = new jsPDF({
                orientation: 'portrait',
                unit: 'mm',
                format: 'a4'
            });

            // استخدام الخط العربي
            doc.setFont('Cairo');

            doc.setFontSize(20);
            doc.text('تقرير الإصابة النباتية', 105, 20, { align: 'center' });

            doc.setFontSize(14);
            let y = 40;

            const addLine = (label, value) => {
                if (value) {
                    doc.text(`${label}: ${value}`, 20, y);
                    y += 15;
                }
            };

            addLine('تاريخ الاكتشاف', r.date);
            addLine('اسم الإصابة', r.pestName);
            addLine('الاسم العلمي', r.scientificName);
            addLine('المحصول', r.affectedCrop);

            doc.text('الأعراض:', 20, y); y += 8;
            const symptoms = doc.splitTextToSize(r.symptoms, 170);
            doc.text(symptoms, 20, y); y += symptoms.length * 6 + 10;

            addLine('المبيد', r.pesticide);
            if (r.notes) {
                doc.text('ملاحظات:', 20, y); y += 8;
                const notes = doc.splitTextToSize(r.notes, 170);
                doc.text(notes, 20, y); y += notes.length * 6 + 10;
            }

            if (r.images && r.images.length > 0) {
                doc.addPage();
                doc.text('صور الإصابة', 20, 20);
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
            Object.assign(document, {
                'discovery-date': r.date,
                'pest-name': r.pestName,
                'scientific-name': r.scientificName || '',
                'affected-crop': r.affectedCrop,
                'symptoms': r.symptoms,
                'pesticide': r.pesticide || '',
                'notes': r.notes || ''
            });
            document.getElementById('captured-images').innerHTML = '';
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
            const term = document.getElementById('search-input').value.toLowerCase();
            if (!term) return renderRecordsTable();
            const results = records.filter(r =>
                Object.values(r).some(v => String(v).toLowerCase().includes(term))
            );
            renderSearchResults(results);
        }

        function renderSearchResults(results) {
            const tbody = document.getElementById('records-table-body');
            tbody.innerHTML = results.map(r => `
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
            `).join('');
            document.getElementById('no-records').classList.add('hidden');
            document.getElementById('pagination').innerHTML = '';
        }
    </script>
</body>
</html>
