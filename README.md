<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no"/>
  <meta name="theme-color" content="#27ae60">
  <title>زراعتي - تطبيق الزراعة الذكي</title>
  <link rel="manifest" href="manifest.json">
  <style>
    :root {
      --primary: #27ae60;
      --light: #f4f8f7;
      --dark: #2c3e50;
      --shadow: 0 4px 12px rgba(0,0,0,0.1);
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: 'Segoe UI', 'Tahoma', sans-serif;
    }

    body {
      background-color: var(--light);
      color: var(--dark);
      line-height: 1.6;
    }

    .container {
      max-width: 1200px;
      margin: 20px auto;
      padding: 15px;
    }

    header {
      text-align: center;
      margin-bottom: 20px;
    }

    header h1 {
      color: var(--primary);
      font-size: 1.8rem;
    }

    .search-box {
      width: 100%;
      padding: 14px;
      font-size: 16px;
      border: 1px solid #bdc3c7;
      border-radius: 12px;
      margin-bottom: 20px;
      outline: none;
    }

    .btn {
      background-color: var(--primary);
      color: white;
      border: none;
      padding: 12px 20px;
      font-size: 16px;
      border-radius: 10px;
      cursor: pointer;
    }

    .btn:hover {
      background-color: #219653;
    }

    .btn-danger {
      background-color: #e74c3c;
    }

    .btn-danger:hover {
      background-color: #c0392b;
    }

    .btn-sm {
      padding: 6px 12px;
      font-size: 14px;
    }

    .add-btn {
      text-align: center;
      margin-bottom: 20px;
    }

    .crops-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
      gap: 20px;
    }

    .crop-card {
      background: white;
      border-radius: 14px;
      overflow: hidden;
      box-shadow: var(--shadow);
      cursor: pointer;
      transition: transform 0.3s;
    }

    .crop-card:hover {
      transform: translateY(-5px);
    }

    .crop-img-container {
      height: 150px;
      overflow: hidden;
    }

    .crop-img-container img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }

    .crop-info {
      padding: 15px;
    }

    .crop-name {
      font-weight: bold;
      color: var(--primary);
      margin-bottom: 5px;
    }

    .crop-scientific {
      font-size: 0.9rem;
      color: #666;
    }

    .crop-actions {
      display: flex;
      gap: 5px;
      margin-top: 10px;
    }

    /* نافذة الإضافة/التعديل */
    .modal {
      display: none;
      position: fixed;
      z-index: 1000;
      left: 0;
      top: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0,0,0,0.5);
      overflow-y: auto;
      padding: 20px;
    }

    .modal-content {
      background-color: white;
      margin: 5% auto;
      padding: 25px;
      border-radius: 16px;
      width: 90%;
      max-width: 600px;
      box-shadow: 0 10px 30px rgba(0,0,0,0.2);
    }

    .modal-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 20px;
      border-bottom: 1px solid #eee;
    }

    .modal-header h2 {
      color: var(--primary);
    }

    .close {
      font-size: 28px;
      font-weight: bold;
      color: #aaa;
      cursor: pointer;
    }

    .close:hover {
      color: #000;
    }

    .form-group {
      margin-bottom: 18px;
    }

    .form-group label {
      display: block;
      margin-bottom: 6px;
      font-weight: bold;
    }

    .form-group input,
    .form-group textarea {
      width: 100%;
      padding: 12px;
      border: 1px solid #bdc3c7;
      border-radius: 8px;
      font-size: 16px;
      outline: none;
    }

    .preview-container {
      display: flex;
      gap: 10px;
      margin-top: 10px;
      flex-wrap: wrap;
    }

    .preview-img {
      width: 100px;
      height: 100px;
      object-fit: cover;
      border-radius: 8px;
      border: 2px solid var(--primary);
    }

    .preview-box {
      display: none;
      flex-direction: column;
      gap: 5px;
    }

    /* تفاصيل المحصول */
    .detail-content {
      background: #f8f9fa;
      padding: 20px;
      border-radius: 12px;
      margin-bottom: 20px;
    }

    .detail-imgs {
      display: flex;
      gap: 10px;
      margin-bottom: 15px;
      flex-wrap: wrap;
    }

    .detail-img {
      width: 100%;
      height: 180px;
      object-fit: cover;
      border-radius: 10px;
    }

    .img-label {
      font-weight: bold;
      color: var(--primary);
      margin: 10px 0 5px;
    }

    .detail-row {
      display: flex;
      margin-bottom: 12px;
    }

    .detail-label {
      font-weight: bold;
      color: var(--primary);
      min-width: 130px;
    }

    .detail-value {
      flex: 1;
    }

    .detail-actions {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
    }

    /* قالب PDF */
    #pdfContainer {
      position: absolute;
      top: -9999px;
      left: -9999px;
      width: 210mm;
      min-height: 297mm;
      background: white;
      padding: 25px;
      box-sizing: border-box;
      direction: rtl;
      font-family: 'Segoe UI', sans-serif;
      z-index: -1;
    }

    .pdf-img {
      width: 100%;
      max-width: 160px;
      height: auto;
      border: 1px solid #ddd;
      border-radius: 8px;
    }
  </style>
</head>
<body>

  <div class="container">
    <header>
      <h1>زراعتي 🌿</h1>
      <p>تطبيق إدارة المحاصيل الذكي</p>
    </header>

    <input type="text" id="searchInput" class="search-box" placeholder="ابحث عن محصول..." />

    <div class="add-btn">
      <button id="addCropBtn" class="btn">➕ إضافة محصول</button>
    </div>

    <div id="cropsList" class="crops-grid"></div>
  </div>

  <!-- نافذة الإضافة/التعديل -->
  <div id="cropModal" class="modal">
    <div class="modal-content">
      <div class="modal-header">
        <h2 id="modalTitle">إضافة محصول جديد</h2>
        <span class="close">&times;</span>
      </div>
      <form id="cropForm">
        <div class="form-group">
          <label>صورة عامة للنبتة</label>
          <input type="file" id="plantImage" accept="image/*" />
          <div class="preview-box" id="plantPreviewBox">
            <span>النبتة</span>
            <img id="plantPreview" class="preview-img" src="" alt="صورة النبتة" />
          </div>
        </div>
        <div class="form-group">
          <label>صورة الزهرة</label>
          <input type="file" id="flowerImage" accept="image/*" />
          <div class="preview-box" id="flowerPreviewBox">
            <span>الزهرة</span>
            <img id="flowerPreview" class="preview-img" src="" alt="صورة الزهرة" />
          </div>
        </div>
        <div class="form-group">
          <label>صورة الثمرة</label>
          <input type="file" id="fruitImage" accept="image/*" />
          <div class="preview-box" id="fruitPreviewBox">
            <span>الثمرة</span>
            <img id="fruitPreview" class="preview-img" src="" alt="صورة الثمرة" />
          </div>
        </div>
        <div class="form-group">
          <label>الاسم المحلي *</label>
          <input type="text" id="localName" required />
        </div>
        <div class="form-group">
          <label>الاسم العلمي</label>
          <input type="text" id="scientificName" />
        </div>
        <div class="form-group">
          <label>فترة التزهير</label>
          <input type="text" id="floweringPeriod" />
        </div>
        <div class="form-group">
          <label>فترة الثمار</label>
          <input type="text" id="fruitingPeriod" />
        </div>
        <div class="form-group">
          <label>عائلة النبتة</label>
          <input type="text" id="family" />
        </div>
        <div class="form-group">
          <label>عمر النبتة</label>
          <input type="text" id="lifespan" />
        </div>
        <div class="form-group">
          <label>الموقع</label>
          <input type="text" id="location" />
        </div>
        <div class="form-group">
          <label>احتياج التسميد</label>
          <textarea id="fertilizationNeeds" rows="3"></textarea>
        </div>
        <button type="submit" class="btn">💾 حفظ المحصول</button>
      </form>
    </div>
  </div>

  <!-- نافذة التفاصيل -->
  <div id="detailModal" class="modal">
    <div class="modal-content">
      <div class="modal-header">
        <h2 id="detailTitle">تفاصيل المحصول</h2>
        <span class="close-detail">&times;</span>
      </div>
      <div id="detailContent" class="detail-content"></div>
      <div class="detail-actions">
        <button id="editCropBtn" class="btn btn-sm">✏️ تعديل</button>
        <button id="deleteCropBtn" class="btn btn-sm btn-danger">🗑️ حذف</button>
        <button id="copyToClipboard" class="btn btn-sm">📋 نسخ</button>
        <button id="downloadPdfBtn" class="btn">تنزيل كـ PDF</button>
      </div>
    </div>
  </div>

  <!-- قالب PDF -->
  <div id="pdfContainer"></div>

  <!-- تحميل المكتبات -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>

  <script>
    // التحقق من دعم localStorage
    if (typeof localStorage === 'undefined') {
      alert('متصفحك لا يدعم التخزين المحلي.');
    }

    // تسجيل Service Worker
    if ('serviceWorker' in navigator) {
      window.addEventListener('load', () => {
        navigator.serviceWorker.register('service-worker.js').catch(() => {});
      });
    }

    // المتغيرات
    let crops = JSON.parse(localStorage.getItem('crops') || '[]');
    let currentCropId = null;

    const searchInput = document.getElementById('searchInput');
    const cropsList = document.getElementById('cropsList');
    const addCropBtn = document.getElementById('addCropBtn');
    const cropModal = document.getElementById('cropModal');
    const detailModal = document.getElementById('detailModal');
    const cropForm = document.getElementById('cropForm');
    const pdfContainer = document.getElementById('pdfContainer');

    // عناصر الصور
    const plantImage = document.getElementById('plantImage');
    const flowerImage = document.getElementById('flowerImage');
    const fruitImage = document.getElementById('fruitImage');

    const plantPreview = document.getElementById('plantPreview');
    const flowerPreview = document.getElementById('flowerPreview');
    const fruitPreview = document.getElementById('fruitPreview');

    const plantPreviewBox = document.getElementById('plantPreviewBox');
    const flowerPreviewBox = document.getElementById('flowerPreviewBox');
    const fruitPreviewBox = document.getElementById('fruitPreviewBox');

    // عرض الصور
    function setupImagePreview(input, preview, box) {
      input.addEventListener('change', () => {
        const file = input.files[0];
        if (file) {
          const reader = new FileReader();
          reader.onload = (e) => {
            preview.src = e.target.result;
            preview.style.display = 'block';
            box.style.display = 'flex';
          };
          reader.onerror = () => alert('فشل تحميل الصورة');
          reader.readAsDataURL(file);
        }
      });
    }

    setupImagePreview(plantImage, plantPreview, plantPreviewBox);
    setupImagePreview(flowerImage, flowerPreview, flowerPreviewBox);
    setupImagePreview(fruitImage, fruitPreview, fruitPreviewBox);

    // فتح/إغلاق النافذات
    addCropBtn.onclick = () => openCropModal();
    document.querySelector('.close')?.addEventListener('click', () => cropModal.style.display = 'none');
    document.querySelector('.close-detail')?.addEventListener('click', () => detailModal.style.display = 'none');
    window.onclick = (e) => {
      if (e.target === cropModal) cropModal.style.display = 'none';
      if (e.target === detailModal) detailModal.style.display = 'none';
    };

    // فتح نافذة الإضافة أو التعديل
    function openCropModal(crop = null) {
      cropForm.reset();
      plantPreviewBox.style.display = 'none';
      flowerPreviewBox.style.display = 'none';
      fruitPreviewBox.style.display = 'none';

      document.getElementById('modalTitle').textContent = crop ? 'تعديل المحصول' : 'إضافة محصول جديد';
      currentCropId = crop ? crop.id : null;

      if (crop) {
        document.getElementById('localName').value = crop.localName;
        document.getElementById('scientificName').value = crop.scientificName || '';
        document.getElementById('floweringPeriod').value = crop.floweringPeriod || '';
        document.getElementById('fruitingPeriod').value = crop.fruitingPeriod || '';
        document.getElementById('family').value = crop.family || '';
        document.getElementById('lifespan').value = crop.lifespan || '';
        document.getElementById('location').value = crop.location || '';
        document.getElementById('fertilizationNeeds').value = crop.fertilizationNeeds || '';

        // عرض الصور الحالية
        if (crop.plantImage) {
          plantPreview.src = crop.plantImage;
          plantPreviewBox.style.display = 'flex';
        }
        if (crop.flowerImage) {
          flowerPreview.src = crop.flowerImage;
          flowerPreviewBox.style.display = 'flex';
        }
        if (crop.fruitImage) {
          fruitPreview.src = crop.fruitImage;
          fruitPreviewBox.style.display = 'flex';
        }
      }
      cropModal.style.display = 'block';
    }

    // ضغط الصورة
    function compressImage(file, maxWidth = 800) {
      return new Promise(resolve => {
        const img = new Image();
        img.onload = () => {
          const canvas = document.createElement('canvas');
          const ctx = canvas.getContext('2d');
          let width = img.width;
          let height = img.height;
          if (width > maxWidth) {
            height = Math.round((height * maxWidth) / width);
            width = maxWidth;
          }
          canvas.width = width;
          canvas.height = height;
          ctx.drawImage(img, 0, 0, width, height);
          canvas.toBlob(blob => {
            const compressed = new File([blob], file.name, { type: 'image/jpeg' });
            resolve(compressed);
          }, 'image/jpeg', 0.7);
        };
        img.src = URL.createObjectURL(file);
      });
    }

    // تحويل الصورة إلى Base64
    function toBase64(file) {
      return new Promise((resolve, reject) => {
        const reader = new FileReader();
        reader.onload = () => resolve(reader.result);
        reader.onerror = () => reject(new Error('فشل قراءة الملف'));
        reader.readAsDataURL(file);
      });
    }

    // حفظ المحصول
    cropForm.addEventListener('submit', async (e) => {
      e.preventDefault();

      const localName = document.getElementById('localName').value.trim();
      if (!localName) {
        alert('الاسم المحلي مطلوب');
        return;
      }

      const plantFile = plantImage.files[0];
      const flowerFile = flowerImage.files[0];
      const fruitFile = fruitImage.files[0];

      let plantImageURL = currentCropId ? (crops.find(c => c.id === currentCropId)?.plantImage || '') : '';
      let flowerImageURL = currentCropId ? (crops.find(c => c.id === currentCropId)?.flowerImage || '') : '';
      let fruitImageURL = currentCropId ? (crops.find(c => c.id === currentCropId)?.fruitImage || '') : '';

      if (plantFile) {
        try {
          const compressed = await compressImage(plantFile);
          plantImageURL = await toBase64(compressed);
        } catch (error) {
          alert('فشل تحميل صورة النبتة');
        }
      }
      if (flowerFile) {
        try {
          const compressed = await compressImage(flowerFile);
          flowerImageURL = await toBase64(compressed);
        } catch (error) {
          alert('فشل تحميل صورة الزهرة');
        }
      }
      if (fruitFile) {
        try {
          const compressed = await compressImage(fruitFile);
          fruitImageURL = await toBase64(compressed);
        } catch (error) {
          alert('فشل تحميل صورة الثمرة');
        }
      }

      const cropData = {
        id: currentCropId || Date.now().toString(),
        localName,
        scientificName: document.getElementById('scientificName').value,
        floweringPeriod: document.getElementById('floweringPeriod').value,
        fruitingPeriod: document.getElementById('fruitingPeriod').value,
        family: document.getElementById('family').value,
        lifespan: document.getElementById('lifespan').value,
        location: document.getElementById('location').value,
        fertilizationNeeds: document.getElementById('fertilizationNeeds').value,
        plantImage: plantImageURL,
        flowerImage: flowerImageURL,
        fruitImage: fruitImageURL,
      };

      if (currentCropId) {
        crops = crops.map(c => c.id === currentCropId ? cropData : c);
      } else {
        crops.push(cropData);
      }

      try {
        localStorage.setItem('crops', JSON.stringify(crops));
        cropModal.style.display = 'none';
        renderCrops();
        alert('تم الحفظ بنجاح!');
      } catch (e) {
        alert('فشل الحفظ. الجهاز ممتلئ أو المتصفح قديم.');
      }
    });

    // حذف المحصول
    function deleteCrop(id) {
      if (confirm('هل أنت متأكد من الحذف؟')) {
        crops = crops.filter(c => c.id !== id);
        localStorage.setItem('crops', JSON.stringify(crops));
        detailModal.style.display = 'none';
        renderCrops();
        alert('تم الحذف بنجاح!');
      }
    }

    // عرض المحاصيل
    function renderCrops() {
      const term = searchInput.value.toLowerCase();
      cropsList.innerHTML = '';
      const filtered = crops.filter(crop =>
        crop.localName.toLowerCase().includes(term) ||
        (crop.scientificName && crop.scientificName.toLowerCase().includes(term))
      );

      if (filtered.length === 0) {
        cropsList.innerHTML = `
          <div style="grid-column: 1 / -1; text-align: center; color: #777; padding: 40px;">
            <p>لا توجد محاصيل. أضف واحدًا!</p>
          </div>`;
        return;
      }

      filtered.forEach(crop => {
        const div = document.createElement('div');
        div.className = 'crop-card';
        div.innerHTML = `
          <div class="crop-img-container">
            <img src="${crop.plantImage || crop.flowerImage || crop.fruitImage || 'https://via.placeholder.com/300x150?text=لا+صورة'}" alt="${crop.localName}" />
          </div>
          <div class="crop-info">
            <div class="crop-name">${crop.localName}</div>
            <div class="crop-scientific">${crop.scientificName || 'لا يوجد اسم علمي'}</div>
            <div class="crop-actions">
              <button data-id="${crop.id}" class="edit-btn btn btn-sm">✏️</button>
              <button data-id="${crop.id}" class="delete-btn btn btn-sm btn-danger">🗑️</button>
            </div>
          </div>
        `;
        div.querySelector('.edit-btn').onclick = (e) => {
          e.stopPropagation();
          openCropModal(crops.find(c => c.id === e.target.dataset.id));
        };
        div.querySelector('.delete-btn').onclick = (e) => {
          e.stopPropagation();
          deleteCrop(e.target.dataset.id);
        };
        div.onclick = () => showCropDetail(crop);
        cropsList.appendChild(div);
      });
    }

    // عرض التفاصيل
    function showCropDetail(crop) {
      currentCropId = crop.id;
      const detailContent = document.getElementById('detailContent');
      let imagesHtml = '';
      if (crop.plantImage || crop.flowerImage || crop.fruitImage) {
        imagesHtml += '<div class="detail-imgs">';
        if (crop.plantImage) {
          imagesHtml += `<div><div class="img-label">صورة النبتة</div><img src="${crop.plantImage}" class="detail-img" alt="صورة النبتة" /></div>`;
        }
        if (crop.flowerImage) {
          imagesHtml += `<div><div class="img-label">صورة الزهرة</div><img src="${crop.flowerImage}" class="detail-img" alt="صورة الزهرة" /></div>`;
        }
        if (crop.fruitImage) {
          imagesHtml += `<div><div class="img-label">صورة الثمرة</div><img src="${crop.fruitImage}" class="detail-img" alt="صورة الثمرة" /></div>`;
        }
        imagesHtml += '</div>';
      }

      detailContent.innerHTML = `
        ${imagesHtml}
        <div class="detail-row">
          <div class="detail-label">الاسم المحلي:</div>
          <div class="detail-value">${crop.localName}</div>
        </div>
        <div class="detail-row">
          <div class="detail-label">الاسم العلمي:</div>
          <div class="detail-value">${crop.scientificName || 'غير محدد'}</div>
        </div>
        <div class="detail-row">
          <div class="detail-label">فترة التزهير:</div>
          <div class="detail-value">${crop.floweringPeriod || 'غير محدد'}</div>
        </div>
        <div class="detail-row">
          <div class="detail-label">فترة الثمار:</div>
          <div class="detail-value">${crop.fruitingPeriod || 'غير محدد'}</div>
        </div>
        <div class="detail-row">
          <div class="detail-label">عائلة النبتة:</div>
          <div class="detail-value">${crop.family || 'غير محدد'}</div>
        </div>
        <div class="detail-row">
          <div class="detail-label">عمر النبتة:</div>
          <div class="detail-value">${crop.lifespan || 'غير محدد'}</div>
        </div>
        <div class="detail-row">
          <div class="detail-label">الموقع:</div>
          <div class="detail-value">${crop.location || 'غير محدد'}</div>
        </div>
        <div class="detail-row">
          <div class="detail-label">احتياج التسميد:</div>
          <div class="detail-value">${crop.fertilizationNeeds || 'غير محدد'}</div>
        </div>
      `;
      document.getElementById('detailTitle').textContent = crop.localName;
      detailModal.style.display = 'block';
    }

    // نسخ التفاصيل
    document.getElementById('copyToClipboard').addEventListener('click', () => {
      const text = document.getElementById('detailContent').innerText;
      navigator.clipboard.writeText(text).then(() => {
        alert('تم النسخ إلى الحافظة!');
      }).catch(() => alert('فشل النسخ'));
    });

    // تعديل
    document.getElementById('editCropBtn').addEventListener('click', () => {
      const crop = crops.find(c => c.id === currentCropId);
      openCropModal(crop);
      detailModal.style.display = 'none';
    });

    // حذف
    document.getElementById('deleteCropBtn').addEventListener('click', () => {
      deleteCrop(currentCropId);
    });

    // تنزيل كـ PDF (احترافي)
    document.getElementById('downloadPdfBtn').addEventListener('click', async () => {
      const crop = crops.find(c => c.id === currentCropId);
      if (!crop) return;

      const { jsPDF } = window.jspdf;
      const pdf = new jsPDF({
        orientation: 'portrait',
        unit: 'mm',
        format: 'a4'
      });

      // إعداد القالب
      pdfContainer.innerHTML = `
        <div style="text-align: center; margin-bottom: 30px;">
          <h1 style="color: #27ae60; font-size: 24px; margin: 0;">تقرير المحصول</h1>
          <h2 style="font-size: 20px; margin: 10px 0;">${crop.localName}</h2>
        </div>
        <div style="display: flex; gap: 20px; justify-content: center; flex-wrap: wrap; margin-bottom: 20px;">
          ${crop.plantImage ? `<div><div style="font-weight:bold; margin-bottom:8px;">صورة النبتة</div><img src="${crop.plantImage}" class="pdf-img" /></div>` : ''}
          ${crop.flowerImage ? `<div><div style="font-weight:bold; margin-bottom:8px;">صورة الزهرة</div><img src="${crop.flowerImage}" class="pdf-img" /></div>` : ''}
          ${crop.fruitImage ? `<div><div style="font-weight:bold; margin-bottom:8px;">صورة الثمرة</div><img src="${crop.fruitImage}" class="pdf-img" /></div>` : ''}
        </div>
        <div style="margin: 20px 0; line-height: 2; font-size: 14px;">
          <p><strong>الاسم المحلي:</strong> ${crop.localName}</p>
          <p><strong>الاسم العلمي:</strong> ${crop.scientificName || 'غير محدد'}</p>
          <p><strong>فترة التزهير:</strong> ${crop.floweringPeriod || 'غير محدد'}</p>
          <p><strong>فترة الثمار:</strong> ${crop.fruitingPeriod || 'غير محدد'}</p>
          <p><strong>عائلة النبتة:</strong> ${crop.family || 'غير محدد'}</p>
          <p><strong>عمر النبتة:</strong> ${crop.lifespan || 'غير محدد'}</p>
          <p><strong>الموقع:</strong> ${crop.location || 'غير محدد'}</p>
          <p><strong>احتياج التسميد:</strong> ${crop.fertilizationNeeds || 'غير محدد'}</p>
        </div>
        <div style="text-align: center; margin-top: 40px; color: #666; font-size: 12px; border-top: 1px solid #eee; padding-top: 15px;">
          تم إنشاء هذا التقرير باستخدام تطبيق زراعتي الذكي
        </div>
      `;

      try {
        const imgElements = pdfContainer.querySelectorAll('img');
        if (imgElements.length > 0) {
          await Promise.all(Array.from(imgElements).map(img => {
            return new Promise((resolve) => {
              if (img.complete) resolve();
              else img.onload = resolve;
            });
          }));
        }

        const canvas = await html2canvas(pdfContainer, {
          scale: 3,
          useCORS: true,
          backgroundColor: 'white'
        });

        const imgData = canvas.toDataURL('image/jpeg', 0.9);
        const width = pdf.internal.pageSize.getWidth();
        const height = (canvas.height * width) / canvas.width;

        pdf.addImage(imgData, 'JPEG', 0, 0, width, height);
        pdf.save(`${crop.localName}.pdf`);

        pdfContainer.innerHTML = '';

      } catch (error) {
        console.error('خطأ في إنشاء PDF:', error);
        alert('فشل إنشاء PDF. تأكد من اتصال الإنترنت وحاول مرة أخرى.');
      }
    });

    // بحث
    searchInput.addEventListener('input', renderCrops);

    // تحميل المحاصيل
    renderCrops();
  </script>
</body>
</html>
