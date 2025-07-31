<موقع تجريبي>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <meta name="theme-color" content="#27ae60">
  <title>زراعتي - تطبيق الزراعة الذكي</title>
  <link rel="manifest" href="manifest.json">
  <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Tajawal:wght@400;500;700&display=swap">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
  <style>
    :root {
      --primary: #27ae60;
      --primary-dark: #219653;
      --light: #f4f8f7;
      --dark: #2c3e50;
      --gray: #95a5a6;
      --danger: #e74c3c;
      --warning: #f39c12;
      --info: #3498db;
      --shadow: 0 4px 12px rgba(0,0,0,0.1);
      --radius: 12px;
    }

    body.dark-mode {
      --light: #1a1a1a;
      --dark: #f0f0f0;
      --gray: #aaa;
      background-color: #1a1a1a;
      color: #f0f0f0;
    }

    body.dark-mode .crop-card,
    body.dark-mode .stat-card,
    body.dark-mode .modal-content,
    body.dark-mode .detail-content,
    body.dark-mode .search-box,
    body.dark-mode .form-control,
    body.dark-mode .image-preview {
      background: #2d2d2d;
      border-color: #444;
      color: #f0f0f0;
    }

    body.dark-mode .alert-success {
      background-color: #1e3e2e;
      border-color: #1a5533;
      color: #4cd97b;
    }

    body.dark-mode .alert-danger {
      background-color: #4a2422;
      border-color: #884440;
      color: #ff6b6b;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: 'Tajawal', sans-serif;
      transition: background-color 0.3s, color 0.3s;
    }

    body {
      background-color: var(--light);
      color: var(--dark);
      line-height: 1.6;
      min-height: 100vh;
    }

    .container {
      max-width: 1200px;
      margin: 0 auto;
      padding: 15px;
    }

    header {
      text-align: center;
      margin-bottom: 20px;
      padding: 15px 0;
      position: relative;
    }

    header h1 {
      color: var(--primary);
      font-size: 2rem;
      margin-bottom: 5px;
    }

    header p {
      color: var(--gray);
    }

    .user-menu {
      position: absolute;
      left: 15px;
      top: 15px;
    }

    .theme-toggle {
      background: none;
      border: none;
      color: var(--primary);
      font-size: 1.2em;
      cursor: pointer;
    }

    .search-box {
      width: 100%;
      padding: 14px 20px;
      font-size: 16px;
      border: 1px solid #bdc3c7;
      border-radius: var(--radius);
      margin-bottom: 20px;
      outline: none;
      transition: all 0.3s;
    }

    .search-box:focus {
      border-color: var(--primary);
      box-shadow: 0 0 0 2px rgba(39, 174, 96, 0.2);
    }

    .btn {
      background-color: var(--primary);
      color: white;
      border: none;
      padding: 12px 20px;
      font-size: 16px;
      border-radius: var(--radius);
      cursor: pointer;
      transition: all 0.3s;
      display: inline-flex;
      align-items: center;
      justify-content: center;
      gap: 8px;
    }

    .btn:hover {
      background-color: var(--primary-dark);
      transform: translateY(-2px);
    }

    .btn-block {
      display: block;
      width: 100%;
    }

    .btn-danger {
      background-color: var(--danger);
    }

    .btn-danger:hover {
      background-color: #c0392b;
    }

    .btn-warning {
      background-color: var(--warning);
    }

    .btn-warning:hover {
      background-color: #d35400;
    }

    .btn-info {
      background-color: var(--info);
    }

    .btn-info:hover {
      background-color: #2980b9;
    }

    .action-buttons {
      display: flex;
      gap: 10px;
      margin-bottom: 20px;
      flex-wrap: wrap;
    }

    .action-buttons .btn {
      flex: 1;
      min-width: 120px;
    }

    .stats-cards {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
      gap: 15px;
      margin-bottom: 20px;
    }

    .stat-card {
      background: white;
      border-radius: var(--radius);
      padding: 15px;
      box-shadow: var(--shadow);
      text-align: center;
    }

    .stat-card h3 {
      color: var(--primary);
      margin-bottom: 5px;
    }

    .stat-card p {
      color: var(--gray);
      font-size: 14px;
    }

    .crops-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
      gap: 20px;
    }

    .crop-card {
      background: white;
      border-radius: var(--radius);
      overflow: hidden;
      box-shadow: var(--shadow);
      cursor: pointer;
      transition: all 0.3s;
      border: 1px solid #e0e0e0;
      position: relative;
    }

    .crop-card:hover {
      transform: translateY(-5px);
      box-shadow: 0 6px 16px rgba(0,0,0,0.15);
    }

    .crop-badge {
      position: absolute;
      top: 10px;
      left: 10px;
      background-color: var(--primary);
      color: white;
      padding: 3px 8px;
      border-radius: 20px;
      font-size: 12px;
      z-index: 2;
    }

    .crop-img-container {
      height: 180px;
      overflow: hidden;
      position: relative;
    }

    .crop-img-container img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      transition: transform 0.5s;
    }

    .crop-card:hover .crop-img-container img {
      transform: scale(1.05);
    }

    .crop-info {
      padding: 15px;
    }

    .crop-name {
      font-weight: bold;
      color: var(--primary);
      font-size: 18px;
      margin-bottom: 5px;
    }

    .crop-scientific {
      color: var(--gray);
      font-size: 14px;
    }

    .crop-meta {
      display: flex;
      justify-content: space-between;
      margin-top: 10px;
      font-size: 12px;
      color: var(--gray);
    }

    /* نافذة التفاصيل */
    .modal {
      display: none;
      position: fixed;
      z-index: 1000;
      left: 0;
      top: 0;
      width: 100%;
      height: 100%;
      background: rgba(0,0,0,0.5);
      overflow: auto;
      backdrop-filter: blur(5px);
    }

    .modal-content {
      background: white;
      margin: 5% auto;
      padding: 25px;
      border-radius: var(--radius);
      width: 90%;
      max-width: 600px;
      box-shadow: 0 10px 30px rgba(0,0,0,0.2);
      position: relative;
      animation: modalFadeIn 0.3s;
    }

    @keyframes modalFadeIn {
      from { opacity: 0; transform: translateY(-20px); }
      to { opacity: 1; transform: translateY(0); }
    }

    .close-btn {
      position: absolute;
      left: 20px;
      top: 20px;
      font-size: 28px;
      cursor: pointer;
      color: var(--gray);
      transition: all 0.3s;
    }

    .close-btn:hover {
      color: var(--dark);
      transform: rotate(90deg);
    }

    .modal-title {
      color: var(--primary);
      text-align: center;
      margin-bottom: 20px;
      font-size: 24px;
    }

    .detail-content {
      background: #f8f9fa;
      padding: 20px;
      border-radius: var(--radius);
      margin-bottom: 20px;
    }

    .detail-img {
      width: 100%;
      height: 250px;
      object-fit: cover;
      border-radius: var(--radius);
      margin-bottom: 20px;
      border: 1px solid #e0e0e0;
    }

    .detail-row {
      display: flex;
      margin-bottom: 12px;
      flex-wrap: wrap;
    }

    .detail-label {
      font-weight: bold;
      color: var(--primary);
      min-width: 130px;
      margin-bottom: 5px;
    }

    .detail-value {
      flex: 1;
    }

    /* نموذج الإضافة/التعديل */
    .form-group {
      margin-bottom: 20px;
    }

    .form-label {
      display: block;
      margin-bottom: 8px;
      font-weight: 500;
      color: var(--dark);
    }

    .form-control {
      width: 100%;
      padding: 12px 15px;
      font-size: 16px;
      border: 1px solid #bdc3c7;
      border-radius: var(--radius);
      transition: all 0.3s;
    }

    .form-control:focus {
      border-color: var(--primary);
      box-shadow: 0 0 0 2px rgba(39, 174, 96, 0.2);
      outline: none;
    }

    textarea.form-control {
      min-height: 100px;
      resize: vertical;
    }

    #map {
      height: 250px;
      width: 100%;
      border-radius: var(--radius);
      margin-top: 15px;
      border: 1px solid #ddd;
    }

    .alert {
      padding: 15px;
      border-radius: var(--radius);
      margin-bottom: 20px;
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .alert-success {
      background-color: #d5f5e3;
      color: #27ae60;
      border: 1px solid #a3e4bf;
    }

    .alert-danger {
      background-color: #fadbd8;
      color: #e74c3c;
      border: 1px solid #f5b7b1;
    }

    .alert-info {
      background-color: #d6eaf8;
      color: #2980b9;
      border: 1px solid #aed6f1;
    }

    @media (max-width: 768px) {
      .crops-grid {
        grid-template-columns: repeat(auto-fill, minmax(240px, 1fr));
      }
      .stats-cards {
        grid-template-columns: 1fr 1fr;
      }
      .modal-content {
        margin: 10% auto;
        width: 95%;
        padding: 20px 15px;
      }
      .detail-row {
        flex-direction: column;
      }
      .detail-label {
        min-width: 100%;
        margin-bottom: 2px;
      }
      .action-buttons .btn {
        min-width: 100%;
      }
      .user-menu {
        position: static;
        margin-bottom: 15px;
        text-align: center;
      }
    }

    #pdfContainer {
      position: absolute;
      top: -9999px;
      left: -9999px;
      width: 210mm;
      min-height: 297mm;
      background: white;
      padding: 20mm;
      box-sizing: border-box;
      direction: rtl;
      font-family: 'Tajawal', sans-serif;
      z-index: -1;
    }

    .image-upload-container {
      display: flex;
      flex-direction: column;
      gap: 10px;
    }

    .image-preview {
      width: 100%;
      height: 150px;
      border: 2px dashed #ddd;
      border-radius: var(--radius);
      display: flex;
      align-items: center;
      justify-content: center;
      overflow: hidden;
      position: relative;
    }

    .image-preview img {
      max-width: 100%;
      max-height: 100%;
      object-fit: contain;
    }
  </style>
</head>
<body>

  <div class="container">
    <header>
      <div class="user-menu">
        <button id="userBtn" class="btn btn-info"><i class="fas fa-user"></i> حسابي</button>
        <button id="themeToggle" class="theme-toggle"><i class="fas fa-moon"></i></button>
      </div>
      <h1>زراعتي <i class="fas fa-leaf"></i></h1>
      <p>تطبيق إدارة المحاصيل الذكي</p>
    </header>

    <input type="text" id="searchInput" class="search-box" placeholder="ابحث عن محصول..." />
    
    <div class="stats-cards">
      <div class="stat-card"><h3 id="totalCrops">0</h3><p>إجمالي المحاصيل</p></div>
      <div class="stat-card"><h3 id="floweringCrops">0</h3><p>في مرحلة التزهير</p></div>
      <div class="stat-card"><h3 id="fruitingCrops">0</h3><p>في مرحلة الإثمار</p></div>
      <div class="stat-card"><h3 id="locationsCount">0</h3><p>مواقع مختلفة</p></div>
    </div>

    <div class="action-buttons">
      <button id="addCropBtn" class="btn"><i class="fas fa-plus"></i> إضافة محصول</button>
      <button id="refreshBtn" class="btn btn-warning"><i class="fas fa-sync-alt"></i> تحديث</button>
      <button id="exportAllBtn" class="btn btn-info"><i class="fas fa-file-export"></i> تصدير الكل</button>
    </div>

    <div id="alertContainer"></div>
    <div id="cropsList" class="crops-grid"></div>
  </div>

  <!-- نافذة التفاصيل -->
  <div id="detailModal" class="modal">
    <div class="modal-content">
      <span class="close-btn" id="closeDetail">&times;</span>
      <h2 class="modal-title" id="detailTitle">تفاصيل المحصول</h2>
      <div id="detailContent" class="detail-content"></div>
      <div class="action-buttons">
        <button id="editCropBtn" class="btn"><i class="fas fa-edit"></i> تعديل</button>
        <button id="downloadPdfBtn" class="btn"><i class="fas fa-file-pdf"></i> تنزيل PDF</button>
      </div>
    </div>
  </div>

  <!-- نافذة الإضافة/التعديل -->
  <div id="formModal" class="modal">
    <div class="modal-content">
      <span class="close-btn" id="closeForm">&times;</span>
      <h2 class="modal-title" id="formTitle">إضافة محصول جديد</h2>
      <form id="cropForm">
        <div class="form-group">
          <label class="form-label">صورة المحصول</label>
          <div class="image-upload-container">
            <div class="image-preview" id="imagePreview">
              <span style="color: #95a5a6;">معاينة الصورة</span>
            </div>
            <button type="button" class="btn upload-btn">
              <i class="fas fa-upload"></i> اختر صورة
              <input type="file" id="imageUpload" accept="image/*">
            </button>
          </div>
          <input type="text" id="imageUrl" class="form-control" style="margin-top:10px;" placeholder="أو أدخل رابط الصورة">
        </div>

        <div class="form-group">
          <label class="form-label">الاسم المحلي</label>
          <input type="text" id="localName" class="form-control" required>
        </div>
        <div class="form-group">
          <label class="form-label">الاسم العلمي</label>
          <input type="text" id="scientificName" class="form-control">
        </div>
        <div class="form-group">
          <label class="form-label">عائلة النبتة</label>
          <input type="text" id="family" class="form-control">
        </div>
        <div class="form-group">
          <label class="form-label">فترة التزهير</label>
          <input type="text" id="floweringPeriod" class="form-control" placeholder="مثال: من مارس إلى مايو">
        </div>
        <div class="form-group">
          <label class="form-label">فترة الثمار</label>
          <input type="text" id="fruitingPeriod" class="form-control" placeholder="مثال: من يونيو إلى أغسطس">
        </div>
        <div class="form-group">
          <label class="form-label">عمر النبتة</label>
          <input type="text" id="lifespan" class="form-control" placeholder="مثال: سنوي أو معمر">
        </div>
        <div class="form-group">
          <label class="form-label">الموقع</label>
          <input type="text" id="location" class="form-control" placeholder="مثال: الحقل الشمالي">
        </div>
        <div class="form-group">
          <label class="form-label">احتياج التسميد</label>
          <input type="text" id="fertilizationNeeds" class="form-control" placeholder="مثال: كل أسبوعين">
        </div>
        <div class="form-group">
          <label class="form-label">ملاحظات إضافية</label>
          <textarea id="notes" class="form-control"></textarea>
        </div>
        <div class="form-group">
          <label class="form-label">موقع الزراعة (إحداثيات)</label>
          <div id="map"></div>
          <div style="display: flex; gap: 10px; margin-top: 10px;">
            <button type="button" id="getLocationBtn" class="btn" style="flex: 1;"><i class="fas fa-map-marker-alt"></i> تحديد الموقع</button>
            <button type="button" id="clearLocationBtn" class="btn btn-warning" style="flex: 1;"><i class="fas fa-trash-alt"></i> مسح</button>
          </div>
          <input type="hidden" id="latitude">
          <input type="hidden" id="longitude">
        </div>
        <div class="action-buttons">
          <button type="submit" class="btn"><i class="fas fa-save"></i> حفظ</button>
          <button type="button" id="deleteCropBtn" class="btn btn-danger" style="display: none;"><i class="fas fa-trash-alt"></i> حذف</button>
        </div>
      </form>
    </div>
  </div>

  <!-- نافذة المستخدم -->
  <div id="userModal" class="modal">
    <div class="modal-content" style="max-width: 400px;">
      <span class="close-btn" id="closeUserModal">&times;</span>
      <h2 class="modal-title"><i class="fas fa-user-circle"></i> حساب المستخدم</h2>
      <div class="detail-content">
        <div class="detail-row"><div class="detail-label">اسم المستخدم:</div><div class="detail-value" id="usernameDisplay">مزارع</div></div>
        <div class="detail-row"><div class="detail-label">عدد المحاصيل:</div><div class="detail-value" id="userCropsCount">0</div></div>
        <div class="detail-row"><div class="detail-label">تاريخ التسجيل:</div><div class="detail-value" id="registerDate">اليوم</div></div>
      </div>
      <button id="logoutBtn" class="btn btn-danger btn-block"><i class="fas fa-sign-out-alt"></i> تسجيل الخروج</button>
    </div>
  </div>

  <!-- قالب PDF (مخفي) -->
  <div id="pdfContainer"></div>

  <!-- تحميل المكتبات -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
  <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>

  <script>
    // ✅ تهيئة المتغيرات
    let crops = JSON.parse(localStorage.getItem('crops') || '[]');
    let currentUser = JSON.parse(localStorage.getItem('currentUser')) || {
      username: 'مزارع',
      registerDate: new Date().toISOString()
    };
    let currentCropId = null;
    let map = null;
    let marker = null;
    let isEditMode = false;

    // عناصر DOM
    const elements = {
      searchInput: document.getElementById('searchInput'),
      cropsList: document.getElementById('cropsList'),
      addCropBtn: document.getElementById('addCropBtn'),
      refreshBtn: document.getElementById('refreshBtn'),
      exportAllBtn: document.getElementById('exportAllBtn'),
      alertContainer: document.getElementById('alertContainer'),
      userBtn: document.getElementById('userBtn'),
      themeToggle: document.getElementById('themeToggle'),
      // إحصائيات
      totalCrops: document.getElementById('totalCrops'),
      floweringCrops: document.getElementById('floweringCrops'),
      fruitingCrops: document.getElementById('fruitingCrops'),
      locationsCount: document.getElementById('locationsCount'),
      // التفاصيل
      detailModal: document.getElementById('detailModal'),
      closeDetail: document.getElementById('closeDetail'),
      detailContent: document.getElementById('detailContent'),
      detailTitle: document.getElementById('detailTitle'),
      editCropBtn: document.getElementById('editCropBtn'),
      downloadPdfBtn: document.getElementById('downloadPdfBtn'),
      // النموذج
      formModal: document.getElementById('formModal'),
      closeForm: document.getElementById('closeForm'),
      formTitle: document.getElementById('formTitle'),
      cropForm: document.getElementById('cropForm'),
      deleteCropBtn: document.getElementById('deleteCropBtn'),
      getLocationBtn: document.getElementById('getLocationBtn'),
      clearLocationBtn: document.getElementById('clearLocationBtn'),
      // الصور
      imageUpload: document.getElementById('imageUpload'),
      imagePreview: document.getElementById('imagePreview'),
      imageUrl: document.getElementById('imageUrl'),
      // الحقول
      localName: document.getElementById('localName'),
      scientificName: document.getElementById('scientificName'),
      family: document.getElementById('family'),
      floweringPeriod: document.getElementById('floweringPeriod'),
      fruitingPeriod: document.getElementById('fruitingPeriod'),
      lifespan: document.getElementById('lifespan'),
      location: document.getElementById('location'),
      fertilizationNeeds: document.getElementById('fertilizationNeeds'),
      notes: document.getElementById('notes'),
      latitude: document.getElementById('latitude'),
      longitude: document.getElementById('longitude'),
      // المستخدم
      userModal: document.getElementById('userModal'),
      closeUserModal: document.getElementById('closeUserModal'),
      usernameDisplay: document.getElementById('usernameDisplay'),
      userCropsCount: document.getElementById('userCropsCount'),
      registerDate: document.getElementById('registerDate'),
      logoutBtn: document.getElementById('logoutBtn'),
      // PDF
      pdfContainer: document.getElementById('pdfContainer')
    };

    // ✅ دالة العرض
    function showAlert(message, type = 'success') {
      const alert = document.createElement('div');
      alert.className = `alert alert-${type}`;
      alert.innerHTML = `<i class="fas fa-${type === 'success' ? 'check-circle' : 'exclamation-circle'}"></i> ${message}`;
      elements.alertContainer.innerHTML = '';
      elements.alertContainer.appendChild(alert);
      setTimeout(() => {
        alert.style.opacity = '0';
        setTimeout(() => alert.remove(), 300);
      }, 3000);
    }

    // ✅ تهيئة الخريطة
    function initMap(lat = 24.7136, lng = 46.6753) {
      if (map) map.remove();
      map = L.map('map').setView([lat, lng], 13);
      L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
        attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
      }).addTo(map);
      marker = L.marker([lat, lng]).addTo(map).bindPopup('موقع المحصول');
      map.on('click', e => {
        if (!marker) marker = L.marker(e.latlng).addTo(map);
        else marker.setLatLng(e.latlng);
        elements.latitude.value = e.latlng.lat;
        elements.longitude.value = e.latlng.lng;
      });
    }

    // ✅ تحميل الصورة
    elements.imageUpload.addEventListener('change', e => {
      const file = e.target.files[0];
      if (file) {
        const reader = new FileReader();
        reader.onload = () => {
          elements.imagePreview.innerHTML = `<img src="${reader.result}" alt="معاينة">`;
          elements.imageUrl.value = reader.result;
        };
        reader.readAsDataURL(file);
      }
    });

    elements.imageUrl.addEventListener('input', () => {
      if (elements.imageUrl.value) {
        elements.imagePreview.innerHTML = `<img src="${elements.imageUrl.value}" alt="معاينة" onerror="this.parentElement.innerHTML='<span style=color:#95a5a6>فشل التحميل</span>'">`;
      } else {
        elements.imagePreview.innerHTML = '<span style="color: #95a5a6;">معاينة الصورة</span>';
      }
    });

    // ✅ عرض التفاصيل
    function showCropDetail(crop) {
      currentCropId = crop.id;
      let imgHtml = crop.image
        ? `<img src="${crop.image}" class="detail-img" alt="${crop.localName}" onerror="this.onerror=null;this.src='https://via.placeholder.com/600x300?text=صورة+غير+متوفرة'">`
        : `<div style="height:250px;background:#eee;display:flex;align-items:center;justify-content:center;border-radius:12px;margin-bottom:20px;"><p style="color:#777;">لا توجد صورة</p></div>`;

      let detailHTML = imgHtml;
      const fields = [
        ['الاسم المحلي', crop.localName],
        ['الاسم العلمي', crop.scientificName || 'غير محدد'],
        ['عائلة النبتة', crop.family || 'غير محدد'],
        ['فترة التزهير', crop.floweringPeriod || 'غير محدد'],
        ['فترة الثمار', crop.fruitingPeriod || 'غير محدد'],
        ['عمر النبتة', crop.lifespan || 'غير محدد'],
        ['الموقع', crop.location || 'غير محدد'],
        ['احتياج التسميد', crop.fertilizationNeeds || 'غير محدد']
      ];

      fields.forEach(([label, value]) => {
        detailHTML += `<div class="detail-row"><div class="detail-label">${label}:</div><div class="detail-value">${value}</div></div>`;
      });

      if (crop.notes) {
        detailHTML += `<div class="detail-row"><div class="detail-label">ملاحظات:</div><div class="detail-value">${crop.notes}</div></div>`;
      }

      if (crop.latitude && crop.longitude) {
        detailHTML += `<div class="detail-row"><div class="detail-label">الإحداثيات:</div><div class="detail-value">${crop.latitude}, ${crop.longitude}</div></div>`;
      }

      elements.detailContent.innerHTML = detailHTML;
      elements.detailTitle.textContent = crop.localName;
      elements.detailModal.style.display = 'block';
    }

    // ✅ عرض النموذج
    function showCropForm(crop = null) {
      isEditMode = !!crop;
      elements.formTitle.textContent = isEditMode ? 'تعديل المحصول' : 'إضافة محصول جديد';
      elements.deleteCropBtn.style.display = isEditMode ? 'block' : 'none';
      currentCropId = crop?.id || null;

      // إعادة تعيين
      if (!isEditMode) {
        elements.cropForm.reset();
        elements.imagePreview.innerHTML = '<span style="color: #95a5a6;">معاينة الصورة</span>';
      }

      if (crop) {
        elements.imageUrl.value = crop.image || '';
        if (crop.image) elements.imagePreview.innerHTML = `<img src="${crop.image}" alt="معاينة">`;
        elements.localName.value = crop.localName;
        elements.scientificName.value = crop.scientificName || '';
        elements.family.value = crop.family || '';
        elements.floweringPeriod.value = crop.floweringPeriod || '';
        elements.fruitingPeriod.value = crop.fruitingPeriod || '';
        elements.lifespan.value = crop.lifespan || '';
        elements.location.value = crop.location || '';
        elements.fertilizationNeeds.value = crop.fertilizationNeeds || '';
        elements.notes.value = crop.notes || '';
        elements.latitude.value = crop.latitude || '';
        elements.longitude.value = crop.longitude || '';
      }

      const lat = parseFloat(elements.latitude.value) || 24.7136;
      const lng = parseFloat(elements.longitude.value) || 46.6753;
      initMap(lat, lng);

      elements.formModal.style.display = 'block';
    }

    // ✅ حفظ المحصول
    function saveCrop() {
      const data = {
        image: elements.imageUrl.value.trim(),
        localName: elements.localName.value.trim(),
        scientificName: elements.scientificName.value.trim(),
        family: elements.family.value.trim(),
        floweringPeriod: elements.floweringPeriod.value.trim(),
        fruitingPeriod: elements.fruitingPeriod.value.trim(),
        lifespan: elements.lifespan.value.trim(),
        location: elements.location.value.trim(),
        fertilizationNeeds: elements.fertilizationNeeds.value.trim(),
        notes: elements.notes.value.trim(),
        latitude: elements.latitude.value.trim(),
        longitude: elements.longitude.value.trim()
      };

      if (isEditMode) {
        const idx = crops.findIndex(c => c.id === currentCropId);
        if (idx !== -1) crops[idx] = { ...crops[idx], ...data };
        showAlert('تم التحديث بنجاح', 'success');
      } else {
        crops.unshift({
          id: Date.now().toString(),
          createdAt: new Date().toISOString(),
          status: 'growing',
          ...data
        });
        showAlert('تم الإضافة بنجاح', 'success');
      }

      localStorage.setItem('crops', JSON.stringify(crops));
      renderCrops();
      updateStats();
      elements.formModal.style.display = 'none';
    }

    // ✅ عرض المحاصيل
    function renderCrops() {
      const term = elements.searchInput.value.toLowerCase();
      const filtered = crops.filter(c =>
        c.localName.toLowerCase().includes(term) ||
        (c.scientificName && c.scientificName.toLowerCase().includes(term)) ||
        (c.family && c.family.toLowerCase().includes(term)) ||
        (c.location && c.location.toLowerCase().includes(term))
      );

      elements.cropsList.innerHTML = filtered.length === 0
        ? `<div style="grid-column:1/-1;text-align:center;color:#777;padding:40px;"><i class="fas fa-seedling" style="font-size:50px;color:#ddd;"></i><p>لا توجد محاصيل</p></div>`
        : '';

      filtered.forEach(crop => {
        const div = document.createElement('div');
        div.className = 'crop-card';
        const badge = crop.status === 'flowering'
          ? '<div class="crop-badge"><i class="fas fa-spa"></i> تزهير</div>'
          : crop.status === 'fruiting'
            ? '<div class="crop-badge" style="background-color:var(--warning);"><i class="fas fa-apple-alt"></i> إثمار</div>'
            : '';

        div.innerHTML = `${badge}
          <div class="crop-img-container">
            <img src="${crop.image || 'https://via.placeholder.com/300x150?text=لا+توجد+صورة'}" alt="${crop.localName}">
          </div>
          <div class="crop-info">
            <div class="crop-name">${crop.localName}</div>
            <div class="crop-scientific">${crop.scientificName || 'لا يوجد'}</div>
            <div class="crop-meta">
              <span><i class="fas fa-map-marker-alt"></i> ${crop.location || 'غير محدد'}</span>
              <span><i class="far fa-calendar-alt"></i> ${new Date(crop.createdAt).toLocaleDateString('ar-EG')}</span>
            </div>
          </div>`;
        div.onclick = () => showCropDetail(crop);
        elements.cropsList.appendChild(div);
      });
    }

    // ✅ تحميل البيانات
    function initApp() {
      updateStats();
      renderCrops();
      loadUserData();
      initEventListeners();

      if (crops.length === 0) {
        crops = [
          { id: '1', localName: 'طماطم', scientificName: 'Solanum lycopersicum', family: 'الباذنجانية', floweringPeriod: '30-45 يوم', fruitingPeriod: '60-90 يوم', lifespan: 'سنوي', location: 'الصوبة 1', fertilizationNeeds: 'كل أسبوعين', image: 'https://upload.wikimedia.org/wikipedia/commons/8/89/Tomato_je.jpg', notes: 'تحتاج ري منتظم', latitude: '24.7136', longitude: '46.6753', createdAt: new Date().toISOString(), status: 'flowering' }
        ];
        localStorage.setItem('crops', JSON.stringify(crops));
        renderCrops();
        updateStats();
      }
    }

    function loadUserData() {
      elements.usernameDisplay.textContent = currentUser.username;
      elements.userCropsCount.textContent = crops.length;
      elements.registerDate.textContent = new Date(currentUser.registerDate).toLocaleDateString('ar-EG');
    }

    function updateStats() {
      elements.totalCrops.textContent = crops.length;
      elements.floweringCrops.textContent = crops.filter(c => c.status === 'flowering').length;
      elements.fruitingCrops.textContent = crops.filter(c => c.status === 'fruiting').length;
      elements.locationsCount.textContent = new Set(crops.map(c => c.location)).size;
    }

    // ✅ التحديد الجغرافي
    elements.getLocationBtn.addEventListener('click', () => {
      if (!navigator.geolocation) return showAlert('المتصفح لا يدعم الموقع', 'danger');
      navigator.geolocation.getCurrentPosition(pos => {
        const { latitude, longitude } = pos.coords;
        elements.latitude.value = latitude;
        elements.longitude.value = longitude;
        if (map) map.setView([latitude, longitude], 15);
        if (marker) marker.setLatLng([latitude, longitude]);
        showAlert('تم تحديد الموقع', 'success');
      }, () => showAlert('فشل الوصول للموقع', 'danger'));
    });

    elements.clearLocationBtn.addEventListener('click', () => {
      if (marker) { map.removeLayer(marker); marker = null; }
      elements.latitude.value = '';
      elements.longitude.value = '';
    });

    // ✅ تبديل الوضع الليلي
    elements.themeToggle.addEventListener('click', () => {
      document.body.classList.toggle('dark-mode');
      elements.themeToggle.innerHTML = document.body.classList.contains('dark-mode') 
        ? '<i class="fas fa-sun"></i>' : '<i class="fas fa-moon"></i>';
    });

    // ✅ الأحداث
    function initEventListeners() {
      elements.addCropBtn.addEventListener('click', () => showCropForm());
      elements.refreshBtn.addEventListener('click', () => { renderCrops(); updateStats(); showAlert('تم التحديث', 'info'); });
      elements.exportAllBtn.addEventListener('click', exportAllCrops);
      elements.closeDetail.addEventListener('click', () => elements.detailModal.style.display = 'none');
      elements.closeForm.addEventListener('click', () => elements.formModal.style.display = 'none');
      elements.closeUserModal.addEventListener('click', () => elements.userModal.style.display = 'none');
      window.addEventListener('click', e => {
        if (e.target === elements.detailModal) elements.detailModal.style.display = 'none';
        if (e.target === elements.formModal) elements.formModal.style.display = 'none';
        if (e.target === elements.userModal) elements.userModal.style.display = 'none';
      });

      elements.editCropBtn.addEventListener('click', () => {
        const crop = crops.find(c => c.id === currentCropId);
        if (crop) { elements.detailModal.style.display = 'none'; showCropForm(crop); }
      });

      elements.downloadPdfBtn.addEventListener('click', generatePdf);
      elements.deleteCropBtn.addEventListener('click', () => {
        if (confirm('حذف؟')) {
          crops = crops.filter(c => c.id !== currentCropId);
          localStorage.setItem('crops', JSON.stringify(crops));
          showAlert('تم الحذف', 'success');
          renderCrops();
          updateStats();
          elements.formModal.style.display = 'none';
          elements.detailModal.style.display = 'none';
        }
      });

      elements.cropForm.addEventListener('submit', e => { e.preventDefault(); saveCrop(); });
      elements.searchInput.addEventListener('input', renderCrops);
      elements.userBtn.addEventListener('click', () => elements.userModal.style.display = 'block');
      elements.logoutBtn.addEventListener('click', () => { showAlert('تم الخروج', 'success'); });
    }

    // ✅ PDF
    async function generatePdf() {
      const crop = crops.find(c => c.id === currentCropId);
      if (!crop) return;
      const { jsPDF } = window.jspdf;
      const pdf = new jsPDF();
      pdf.setFontSize(22);
      pdf.text(`تقرير: ${crop.localName}`, 10, 20);
      pdf.setFontSize(14);
      pdf.text(`الاسم العلمي: ${crop.scientificName || 'غير محدد'}`, 10, 40);
      pdf.text(`الموقع: ${crop.location || 'غير محدد'}`, 10, 50);
      pdf.save(`${crop.localName}.pdf`);
      showAlert('تم تنزيل PDF', 'success');
    }

    async function exportAllCrops() {
      if (crops.length === 0) return showAlert('لا توجد محاصيل', 'warning');
      const { jsPDF } = window.jspdf;
      const pdf = new jsPDF();
      crops.forEach((c, i) => {
        if (i > 0) pdf.addPage();
        pdf.setFontSize(20);
        pdf.text(`المحصول: ${c.localName}`, 10, 20);
        pdf.setFontSize(12);
        pdf.text(`الاسم العلمي: ${c.scientificName || 'غير محدد'}`, 10, 40);
        pdf.text(`الموقع: ${c.location || 'غير محدد'}`, 10, 50);
      });
      pdf.save('جميع_المحاصيل.pdf');
      showAlert('تم التصدير', 'success');
    }

    // ✅ بدء التطبيق
    document.addEventListener('DOMContentLoaded', initApp);
  </script>
</body>
</html>
