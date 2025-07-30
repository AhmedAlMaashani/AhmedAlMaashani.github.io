<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no"/>
  <meta name="theme-color" content="#27ae60">
  <title>زراعتي - تطبيق الزراعة الذكي</title>
  <link rel="manifest" href="manifest.json">
  <style>
    * {
      box-sizing: border-box;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }
    body {
      margin: 0;
      padding: 10px;
      background-color: #f4f8f7;
      color: #2c3e50;
    }
    h1, h2, h3 {
      color: #27ae60;
      margin: 10px 0;
    }
    .container {
      max-width: 900px;
      margin: 0 auto;
      background: white;
      padding: 15px;
      border-radius: 12px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.1);
    }
    .search-box {
      width: 100%;
      padding: 12px;
      font-size: 16px;
      border: 1px solid #bdc3c7;
      border-radius: 8px;
      margin-bottom: 15px;
    }
    .btn {
      background-color: #27ae60;
      color: white;
      border: none;
      padding: 10px 16px;
      font-size: 16px;
      border-radius: 8px;
      cursor: pointer;
      margin: 5px;
    }
    .btn:hover { background-color: #219653; }
    .btn-danger { background-color: #e74c3c; }
    .btn-danger:hover { background-color: #c0392b; }
    .btn-sm { padding: 6px 10px; font-size: 14px; }
    .crop-card {
      border: 1px solid #ecf0f1;
      border-radius: 10px;
      padding: 15px;
      margin-bottom: 15px;
      background: #f9fafa;
      cursor: pointer;
      transition: transform 0.2s;
    }
    .crop-card:hover {
      transform: translateY(-3px);
      box-shadow: 0 6px 12px rgba(0,0,0,0.1);
    }
    .crop-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 10px;
    }
    .crop-image {
      width: 60px;
      height: 60px;
      object-fit: cover;
      border-radius: 8px;
    }
    .crop-info {
      margin-right: 10px;
      flex: 1;
    }
    .crop-name {
      font-weight: bold;
      font-size: 18px;
    }
    .form-group {
      margin-bottom: 15px;
    }
    .form-group label {
      display: block;
      margin-bottom: 5px;
      font-weight: bold;
    }
    .form-group input, .form-group textarea {
      width: 100%;
      padding: 10px;
      border: 1px solid #bdc3c7;
      border-radius: 6px;
      font-size: 16px;
    }
    .modal {
      display: none;
      position: fixed;
      z-index: 1000;
      left: 0; top: 0;
      width: 100%; height: 100%;
      background-color: rgba(0,0,0,0.5);
      overflow-y: auto;
      padding: 20px;
    }
    .modal-content {
      background-color: white;
      margin: 5% auto;
      padding: 20px;
      border-radius: 12px;
      width: 90%;
      max-width: 500px;
      box-shadow: 0 5px 15px rgba(0,0,0,0.3);
    }
    .close {
      float: left;
      font-size: 28px;
      font-weight: bold;
      color: #aaa;
      cursor: pointer;
    }
    .close:hover { color: #000; }
    .crop-detail {
      background: #f8f9fa;
      padding: 20px;
      border-radius: 10px;
      margin-bottom: 15px;
    }
    .detail-row {
      display: flex;
      margin-bottom: 10px;
    }
    .detail-label {
      font-weight: bold;
      color: #27ae60;
      min-width: 130px;
    }
    .action-buttons {
      text-align: left;
      margin-top: 15px;
    }
    @media (max-width: 480px) {
      .container { padding: 10px; }
      .btn { font-size: 14px; padding: 8px 12px; }
      .crop-name { font-size: 16px; }
      .detail-label { min-width: 100px; }
    }
  </style>
</head>
<body>

  <div class="container">
    <h1>زراعتي 🌿</h1>
    <p>تطبيق إدارة المحاصيل الذكي</p>
    <input type="text" id="searchInput" class="search-box" placeholder="ابحث عن محصول..." />
    <button id="addCropBtn" class="btn">➕ إضافة محصول</button>
    <div id="cropsList"></div>
  </div>

  <!-- نافذة إضافة/تعديل -->
  <div id="cropModal" class="modal">
    <div class="modal-content">
      <span class="close">&times;</span>
      <h2 id="modalTitle">إضافة محصول جديد</h2>
      <form id="cropForm">
        <div class="form-group">
          <label>اختر صورة</label>
          <input type="file" id="cropImage" accept="image/*" />
          <img id="preview" src="" alt="معاينة الصورة" style="max-width:100%; margin-top:10px; display:none;">
        </div>
        <div class="form-group">
          <label>الاسم المحلي *</label>
          <input type="text" id="localName" required>
        </div>
        <div class="form-group">
          <label>الاسم العلمي</label>
          <input type="text" id="scientificName">
        </div>
        <div class="form-group">
          <label>فترة التزهير</label>
          <input type="text" id="floweringPeriod">
        </div>
        <div class="form-group">
          <label>فترة الثمار</label>
          <input type="text" id="fruitingPeriod">
        </div>
        <div class="form-group">
          <label>عائلة النبتة</label>
          <input type="text" id="family">
        </div>
        <div class="form-group">
          <label>عمر النبتة</label>
          <input type="text" id="lifespan">
        </div>
        <div class="form-group">
          <label>الموقع</label>
          <input type="text" id="location">
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
      <span class="close-detail">&times;</span>
      <h2 id="detailTitle">تفاصيل المحصول</h2>
      <div id="detailContent" class="crop-detail"></div>
      <div class="action-buttons">
        <button id="editCropBtn" class="btn btn-sm">✏️ تعديل</button>
        <button id="deleteCropBtn" class="btn btn-sm btn-danger">🗑️ حذف</button>
        <button id="copyToClipboard" class="btn btn-sm">📋 نسخ</button>
        <button id="downloadPdfBtn" class="btn">تنزيل كـ PDF</button>
      </div>
    </div>
  </div>

  <!-- قالب مخفي لإنشاء PDF -->
  <div id="pdfTemplate" style="display:none; font-family:sans-serif; direction:rtl; text-align:right; width:180mm; background:white; padding:20px;"></div>

  <!-- تحميل المكتبات -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>

  <script>
    // التحقق من دعم localStorage
    if (typeof localStorage === 'undefined') {
      alert('متصفحك لا يدعم التخزين. استخدم Chrome أو Firefox.');
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
    const preview = document.getElementById('preview');
    const cropImage = document.getElementById('cropImage');
    const pdfTemplate = document.getElementById('pdfTemplate');

    // عرض الصورة المختارة
    cropImage.addEventListener('change', () => {
      const file = cropImage.files[0];
      if (file) {
        const reader = new FileReader();
        reader.onload = (e) => {
          preview.src = e.target.result;
          preview.style.display = 'block';
        };
        reader.onerror = () => alert('فشل تحميل الصورة');
        reader.readAsDataURL(file);
      }
    });

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
      preview.style.display = 'none';
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
        if (crop.image) {
          preview.src = crop.image;
          preview.style.display = 'block';
        }
      }
      cropModal.style.display = 'block';
    }

    // ضغط الصورة قبل التحويل
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
            const compressed = new File([blob], file.name, { type: 'image/jpeg', lastModified: Date.now() });
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

      const file = cropImage.files[0];
      let imageUrl = currentCropId ? crops.find(c => c.id === currentCropId)?.image : '';

      if (file) {
        try {
          const compressedFile = await compressImage(file);
          imageUrl = await toBase64(compressedFile);
        } catch (error) {
          alert('فشل تحميل الصورة. حاول صورة أصغر.');
          console.error('Image error:', error);
          return;
        }
      }

      const cropData = {
        id: currentCropId || Date.now().toString(),
        image: imageUrl,
        localName,
        scientificName: document.getElementById('scientificName').value,
        floweringPeriod: document.getElementById('floweringPeriod').value,
        fruitingPeriod: document.getElementById('fruitingPeriod').value,
        family: document.getElementById('family').value,
        lifespan: document.getElementById('lifespan').value,
        location: document.getElementById('location').value,
        fertilizationNeeds: document.getElementById('fertilizationNeeds').value,
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
        alert('الجهاز ممتلئ أو المتصفح لا يدعم التخزين.');
      }
    });

    // حذف المحصول
    function deleteCrop(id) {
      if (confirm('هل أنت متأكد من حذف هذا المحصول؟')) {
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
        cropsList.innerHTML = '<p>لا توجد محاصيل. أضف واحدًا!</p>';
        return;
      }

      filtered.forEach(crop => {
        const div = document.createElement('div');
        div.className = 'crop-card';
        div.innerHTML = `
          <div class="crop-header">
            <div class="crop-info">
              <div class="crop-name">${crop.localName}</div>
              <small>${crop.scientificName || 'لا يوجد اسم علمي'}</small>
            </div>
            <img src="${crop.image || 'https://via.placeholder.com/60'}" class="crop-image">
          </div>
          <div style="text-align:left; margin-top:10px;">
            <button data-id="${crop.id}" class="edit-btn btn btn-sm">✏️</button>
            <button data-id="${crop.id}" class="delete-btn btn btn-sm btn-danger">🗑️</button>
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
      detailContent.innerHTML = `
        ${crop.image ? `<img src="${crop.image}" style="width:100%; height:120px; object-fit:cover; border-radius:8px; margin-bottom:15px;">` : ''}
        <div class="detail-row"><div class="detail-label">الاسم المحلي:</div> <div>${crop.localName}</div></div>
        <div class="detail-row"><div class="detail-label">الاسم العلمي:</div> <div>${crop.scientificName || 'غير محدد'}</div></div>
        <div class="detail-row"><div class="detail-label">فترة التزهير:</div> <div>${crop.floweringPeriod || 'غير محدد'}</div></div>
        <div class="detail-row"><div class="detail-label">فترة الثمار:</div> <div>${crop.fruitingPeriod || 'غير محدد'}</div></div>
        <div class="detail-row"><div class="detail-label">عائلة النبتة:</div> <div>${crop.family || 'غير محدد'}</div></div>
        <div class="detail-row"><div class="detail-label">عمر النبتة:</div> <div>${crop.lifespan || 'غير محدد'}</div></div>
        <div class="detail-row"><div class="detail-label">الموقع:</div> <div>${crop.location || 'غير محدد'}</div></div>
        <div class="detail-row"><div class="detail-label">احتياج التسميد:</div> <div>${crop.fertilizationNeeds || 'غير محدد'}</div></div>
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

    // تنزيل كـ PDF
    document.getElementById('downloadPdfBtn').addEventListener('click', async () => {
      const crop = crops.find(c => c.id === currentCropId);
      const { jsPDF } = window.jspdf;
      const pdf = new jsPDF({
        orientation: 'portrait',
        unit: 'mm',
        format: 'a4'
      });

      pdfTemplate.innerHTML = `
        <h2 style="text-align:center;">${crop.localName}</h2>
        ${crop.image ? `<img src="${crop.image}" style="width:100%; max-width:150px; display:block; margin:20px auto;">` : ''}
        <p><strong>الاسم المحلي:</strong> ${crop.localName}</p>
        <p><strong>الاسم العلمي:</strong> ${crop.scientificName || 'غير محدد'}</p>
        <p><strong>فترة التزهير:</strong> ${crop.floweringPeriod || 'غير محدد'}</p>
        <p><strong>فترة الثمار:</strong> ${crop.fruitingPeriod || 'غير محدد'}</p>
        <p><strong>عائلة النبتة:</strong> ${crop.family || 'غير محدد'}</p>
        <p><strong>عمر النبتة:</strong> ${crop.lifespan || 'غير محدد'}</p>
        <p><strong>الموقع:</strong> ${crop.location || 'غير محدد'}</p>
        <p><strong>احتياج التسميد:</strong> ${crop.fertilizationNeeds || 'غير محدد'}</p>
      `;

      try {
        const canvas = await html2canvas(pdfTemplate, { scale: 2, useCORS: true, backgroundColor: 'white' });
        const imgData = canvas.toDataURL('image/jpeg', 0.9);
        const width = pdf.internal.pageSize.getWidth();
        const height = (canvas.height * width) / canvas.width;
        pdf.addImage(imgData, 'JPEG', 0, 0, width, height);
        pdf.save(`${crop.localName}.pdf`);
      } catch (error) {
        alert('خطأ في إنشاء PDF. حاول مجددًا.');
      }
    });

    // بحث
    searchInput.addEventListener('input', renderCrops);

    // تحميل المحاصيل
    renderCrops();
  </script>
</body>
</html>
