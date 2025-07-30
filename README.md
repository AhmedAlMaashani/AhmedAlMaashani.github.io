<!DOCTYPE html>
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
      --primary-dark: #219653;
      --danger: #e74c3c;
      --danger-dark: #c0392b;
      --gray: #bdc3c7;
      --light: #f4f8f7;
      --dark: #2c3e50;
      --shadow: 0 4px 12px rgba(0,0,0,0.1);
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: 'Segoe UI', sans-serif;
    }

    body {
      background-color: var(--light);
      color: var(--dark);
      line-height: 1.7;
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
      border: 1px solid var(--gray);
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
      background-color: var(--primary-dark);
    }

    .btn-danger {
      background-color: var(--danger);
    }

    .btn-danger:hover {
      background-color: var(--danger-dark);
    }

    .btn-sm {
      padding: 6px 12px;
      font-size: 14px;
    }

    .add-btn {
      margin-bottom: 20px;
      display: flex;
      justify-content: center;
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

    /* النماذج */
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
      max-width: 520px;
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
      border: 1px solid var(--gray);
      border-radius: 8px;
      font-size: 16px;
      outline: none;
    }

    .form-group textarea {
      min-height: 80px;
      resize: vertical;
    }

    .preview-img {
      max-width: 100%;
      height: 120px;
      object-fit: cover;
      margin-top: 10px;
      border-radius: 8px;
      display: none;
    }

    /* تفاصيل المحصول */
    .detail-content {
      background: #f8f9fa;
      padding: 20px;
      border-radius: 12px;
      margin-bottom: 20px;
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

    .detail-img {
      width: 100%;
      height: 200px;
      object-fit: cover;
      border-radius: 10px;
      margin-bottom: 15px;
    }

    .detail-actions {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
    }

    /* قالب PDF - لا تستخدم display: none */
    #pdfTemplate {
      position: absolute;
      top: -9999px;
      left: -9999px;
      width: 180mm;
      background: white;
      padding: 20px;
      direction: rtl;
      text-align: right;
      font-family: 'Segoe UI', sans-serif;
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

  <!-- نافذة إضافة/تعديل -->
  <div id="cropModal" class="modal">
    <div class="modal-content">
      <div class="modal-header">
        <h2 id="modalTitle">إضافة محصول جديد</h2>
        <span class="close">&times;</span>
      </div>
      <form id="cropForm">
        <div class="form-group">
          <label>اختر صورة</label>
          <input type="file" id="cropImage" accept="image/*" />
          <img id="preview" class="preview-img" src="" alt="معاينة الصورة" />
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

  <!-- قالب PDF (مرئي تقنيًا لكن خارج الشاشة) -->
  <div id="pdfTemplate"></div>

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
    const preview = document.getElementById('preview');
    const cropImage = document.getElementById('cropImage');
    const pdfTemplate = document.getElementById('pdfTemplate');

    // عرض الصورة
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

      const file = cropImage.files[0];
      let imageUrl = currentCropId ? crops.find(c => c.id === currentCropId)?.image : '';

      if (file) {
        try {
          const compressedFile = await compressImage(file);
          imageUrl = await toBase64(compressedFile);
        } catch (error) {
          alert('فشل تحميل الصورة. حاول صورة أصغر.');
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
            <img src="${crop.image || 'https://via.placeholder.com/300x150?text=لا+صورة'}" alt="${crop.localName}" />
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
      detailContent.innerHTML = `
        ${crop.image ? `<img src="${crop.image}" class="detail-img" alt="${crop.localName}" />` : ''}
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

    // تنزيل كـ PDF (الحل النهائي)
    document.getElementById('downloadPdfBtn').addEventListener('click', async () => {
      const crop = crops.find(c => c.id === currentCropId);
      if (!crop) return;

      const { jsPDF } = window.jspdf;
      const pdf = new jsPDF({
        orientation: 'portrait',
        unit: 'mm',
        format: 'a4'
      });

      // ملء قالب PDF
      pdfTemplate.innerHTML = `
        <h2 style="text-align:center; color:#27ae60;">${crop.localName}</h2>
        ${crop.image ? `<img src="${crop.image}" style="width:100%; max-width:150px; display:block; margin:20px auto;" />` : ''}
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
        // الانتظار حتى تحميل الصورة
        const img = pdfTemplate.querySelector('img');
        if (img) {
          await new Promise((resolve) => {
            img.onload = resolve;
            if (img.complete) resolve();
          });
        }

        // التقاط الشاشة
        const canvas = await html2canvas(pdfTemplate, {
          scale: 2,
          useCORS: true,
          backgroundColor: 'white',
          logging: false
        });

        const imgData = canvas.toDataURL('image/jpeg', 0.9);
        const width = pdf.internal.pageSize.getWidth();
        const height = (canvas.height * width) / canvas.width;

        pdf.addImage(imgData, 'JPEG', 0, 0, width, height);
        pdf.save(`${crop.localName}.pdf`);

        // تنظيف القالب
        pdfTemplate.innerHTML = '';

      } catch (error) {
        console.error('خطأ في إنشاء PDF:', error);
        alert('فشل إنشاء PDF. تأكد من اتصال الإنترنت.');
      }
    });

    // بحث
    searchInput.addEventListener('input', renderCrops);

    // تحميل المحاصيل
    renderCrops();
  </script>
</body>
</html>
