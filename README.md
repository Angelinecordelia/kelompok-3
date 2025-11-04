
<html lang="id">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Koperasi Sekolah</title>
  <style>
    :root{
      --primary:#005fa3;
      --accent:#ffcc00;
      --muted:#f7f7f7;
      --text:#222;
      --header-overlay: rgba(0,0,0,0.35);
    }
    *{box-sizing:border-box;margin:0;padding:0}
    html,body{height:100%;font-family:Arial, sans-serif;color:var(--text);background:#fff}
    a{color:inherit;text-decoration:none}

    header.site-header{
      min-height:44vh;
      display:flex;
      flex-direction:column;
      justify-content:center;
      align-items:center;
      text-align:center;
      color:#fff;
      padding:3rem 1rem;
      background-image:
        linear-gradient(var(--header-overlay),var(--header-overlay)),
        url('images/header.jpg');
      background-repeat:no-repeat;
      background-size:cover;
      background-position:center;
      position:relative;
    }
    /* fallback remote image if local not present */
    header.site-header.fallback{
      background-image:
        linear-gradient(var(--header-overlay),var(--header-overlay)),
        url('https://media.licdn.com/dms/image/v2/C4E1BAQGNFPWchaGnig/company-background_10000/company-background_10000/0/1615211173320/smanegeri103jakarta_cover?e=2147483647&v=beta&t=tfU6tdqp73x5EyUuzgUhVTbUtnni5v4DL3rXMy8iZtI');
    }

    /* NAV DI BAWAH HEADER - STYLING SEBAGAI TOMBOL */
    nav.main{
      display:flex;
      justify-content:center;
      width:100%;
      margin-top:-28px; /* naik sedikit agar menyatu visual dengan header */
      z-index:40;
      position:relative;
      padding:0 1rem;
    }
    .nav-inner{
      width:1100px;
      max-width:95%;
      display:flex;
      align-items:center;
      justify-content:center; /* tombol di tengah bawah header */
      gap:0.6rem;
      background: #fff;
      padding:10px;
      border-radius:12px;
      box-shadow:0 6px 18px rgba(0,0,0,0.12);
    }
    .brand{font-weight:700;color:var(--primary);margin-right:6px;display:none}
    .nav-links{list-style:none;display:flex;gap:0.5rem;margin:0;padding:0}
    .nav-links a{
      display:inline-block;
      background:var(--primary);
      color:#fff;
      padding:.6rem .9rem;
      border-radius:8px;
      font-weight:600;
      transition:transform .12s,box-shadow .12s,opacity .12s;
    }
    .nav-links a:hover{transform:translateY(-3px);box-shadow:0 8px 18px rgba(0,0,0,0.12)}
    .nav-links a.active{background:linear-gradient(90deg,var(--primary),#2a8dd6)}

    .header-content h1{font-size:clamp(1.6rem,4vw,2.6rem);margin-bottom:.4rem}
    .header-content p{opacity:.95;margin-bottom:1rem;max-width:820px}
    .btn{background:var(--accent);color:#111;padding:.6rem 1rem;border-radius:8px;font-weight:700}

    main{padding:2rem 1rem;max-width:1100px;margin:0 auto}
    section{margin-bottom:1.6rem;padding:1rem;border-radius:8px}
    .section{display:none;padding:1rem;background:#fff;border-radius:8px;box-shadow:0 6px 18px rgba(0,0,0,.06)}
    .section.active{display:block}
    section#produk .cards{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:1rem;margin-top:1rem}
    .card{background:#fff;padding:1rem;border-radius:8px;box-shadow:0 6px 18px rgba(0,0,0,0.06)}
    .section-alt{background:var(--muted)}

  /* Product details toggle (Alat Tulis) */
  .product-btn{display:inline-block;margin-top:0.6rem;padding:.5rem .8rem;border-radius:8px;background:linear-gradient(90deg,var(--primary),#2a8dd6);color:#fff;border:none;cursor:pointer;font-weight:600}
  .product-btn:focus{outline:2px solid rgba(0,95,163,0.16);outline-offset:3px}
  .details{overflow:hidden;max-height:0;transition:max-height .32s ease,opacity .24s ease;padding:0 .2rem}
  .details.show{max-height:480px;padding-top:.8rem;opacity:1}
  .detail-columns{display:grid;grid-template-columns:1fr 1fr;gap:.6rem}
  .detail-columns ul{list-style:disc;padding-left:1.1rem;color:var(--text);margin:0}
  .detail-columns li{margin:.35rem 0}
  @media (max-width:540px){.detail-columns{grid-template-columns:1fr}}
  /* price table */
  .price-list{margin-top:0.8rem;color:var(--text)}
  .price-table{width:100%;border-collapse:collapse;margin-top:.5rem;font-size:0.98rem}
  .price-table th,.price-table td{padding:.6rem .8rem;border:1px solid rgba(0,0,0,0.06)}
  .price-table thead th{background:rgba(0,0,0,0.03);text-align:left}
  .price-table tbody tr:nth-child(odd){background:rgba(0,0,0,0.02)}
  .price-table td.price{text-align:right;white-space:nowrap}
  .price-wrap{overflow:auto;max-height:320px;-webkit-overflow-scrolling:touch;border:1px solid rgba(0,0,0,0.03);border-radius:6px;padding:.2rem}
  /* Ensure table can be scrolled horizontally on small screens */
  .price-table{min-width:520px}

  /* Modal (popup) styles for product details */
  .modal-overlay{position:fixed;inset:0;background:rgba(2,6,23,0.6);display:none;align-items:center;justify-content:center;z-index:120}
  .modal-overlay.show{display:flex}
  .modal{background:#fff;color:#111;max-width:820px;width:94%;border-radius:12px;box-shadow:0 20px 60px rgba(2,6,23,0.6);overflow:auto;max-height:88vh;padding:1.2rem}
  .modal-header{display:flex;align-items:center;justify-content:space-between;margin-bottom:0.6rem}
  .modal-header h3{margin:0;font-size:1.2rem}
  .modal-close{background:transparent;border:none;font-size:1.2rem;cursor:pointer;padding:.4rem;border-radius:6px}
  .modal-body{color:#333}
  .modal-body .detail-columns{display:block}
  .modal-body ul{margin:.6rem 0;padding-left:1.1rem}
  @media (min-width:640px){.modal-body .detail-columns{display:grid;grid-template-columns:1fr 1fr;gap:1rem}}
  /* Product detail page inside Produk */
  .product-detail{display:none;padding:1rem;border-radius:8px;background:#fff;border:1px solid rgba(0,0,0,0.04);box-shadow:0 6px 18px rgba(0,0,0,0.06);margin-top:1rem}
  .product-detail.active{display:block}
  .product-detail .back{display:inline-block;margin-bottom:0.8rem;color:var(--primary);cursor:pointer}
  .product-detail h3{margin-top:0;margin-bottom:.4rem}

    .contact-list p{margin:.4rem 0}
    footer.site-footer{text-align:center;padding:1rem;color:#666;font-size:.9rem}

    @media (max-width:720px){
      .nav-inner{flex-direction:column;gap:0.4rem;padding:8px}
      .brand{display:none}
      .nav-links{flex-direction:column;align-items:center}
      nav.main{margin-top:-18px}
    }
  </style>
</head>
<body>

  <header class="site-header" id="home" role="banner">
    <div class="header-content">
      <h1>Koperasi SMAN 103 Jakarta</h1>
      <p>Membangun kemandirian dan kesejahteraan warga sekolah — menyediakan alat tulis, seragam, makanan sehat, dan layanan keuangan sederhana untuk siswa & guru.</p>
      
    </div>
  </header>

  <!-- NAV DITEMPATKAN DI BAWAH HEADER -->
  <nav class="main" aria-label="Navigasi utama">
    <div class="nav-inner">
      <div class="brand">Koperasi SMAN 103</div>
      <ul class="nav-links" role="list">
        <li><a href="#tentang" data-target="tentang">Tentang</a></li>
        <li><a href="#produk" data-target="produk">Produk</a></li>
        <li><a href="#anggota" data-target="anggota">Anggota</a></li>
        <li><a href="#kontak" data-target="kontak">Kontak</a></li>
      </ul>
    </div>
  </nav>

  <main>
    <section id="tentang" class="section active">
      <h2>Tentang Koperasi</h2>
      <p>Koperasi SMAN 103 Jakarta merupakan salah satu wadah ekonomi sekolah yang dikelola oleh guru dan siswa untuk mendukung kegiatan belajar sekaligus menanamkan nilai-nilai kemandirian, tanggung jawab, dan kerja sama. Koperasi ini berdiri dengan tujuan utama untuk meningkatkan kesejahteraan anggota, baik siswa, guru, maupun tenaga kependidikan di lingkungan sekolah.Sebagai koperasi sekolah, Koperasi SMAN 103 Jakarta berperan penting dalam menyediakan berbagai kebutuhan siswa, seperti alat tulis, seragam, perlengkapan sekolah, hingga makanan ringan dan minuman sehat di kantin koperasi. Dengan adanya koperasi, siswa tidak perlu keluar lingkungan sekolah untuk memenuhi kebutuhan harian, sehingga lebih efisien dan aman.Koperasi SMAN 103 Jakarta juga rutin mengadakan rapat anggota tahunan (RAT) untuk melaporkan hasil kegiatan dan keuangan selama satu tahun. Dalam rapat tersebut, seluruh anggota diberi kesempatan untuk memberikan saran atau kritik demi kemajuan koperasi ke depannya. Transparansi dan partisipasi aktif anggota menjadi nilai penting dalam menjaga kepercayaan dan kelancaran kegiatan koperasi.</p>
    </section>

    <section id="produk" class="section">
      <h2>Produk & Layanan</h2>
      <div class="cards">
        <article class="card">
          <h3>Alat Tulis</h3>
          <p>Peralatan umum untuk kebutuhan sekolah.</p>
          <button class="product-btn" aria-expanded="false" aria-controls="alat-details">Lihat detail</button>
          <div id="alat-details" class="details" aria-hidden="true">
            <div class="detail-columns">
              <ul>
                <li>Pensil</li>
                <li>Pulpen</li>
                <li>Buku Tulis</li>
                <li>Penggaris</li>
              </ul>
              <ul>
                <li>Penghapus</li>
                <li>Rautan</li>
                <li>Correction Tape</li>
              </ul>
            </div>
          </div>
        </article>
        <article class="card">
          <h3>Seragam & Atribut</h3>
          <p>Seragam olahraga, topi.</p>
          <button class="product-btn" aria-expanded="true" aria-controls="seragam-details">Lihat detail</button>
          <div id="seragam-details" class="details show" aria-hidden="false">
            <div class="detail-columns">
              
            
      
              
              
            
            </div>
            <!-- Daftar harga jual untuk seragam (tabel) -->
            <div class="price-list">
              <h4>Daftar Harga Jual</h4>
              <div class="price-wrap">
                <table class="price-table" role="table" aria-label="Daftar harga jual seragam">
                  <thead>
                    <tr>
                      <th>Item</th>
                      <th>Harga</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr><td>Batik pendek</td><td class="price">Rp140.000,-</td></tr>
                    <tr><td>Batik panjang</td><td class="price">Rp150.000,-</td></tr>
                    <tr><td>Baju koko</td><td class="price">Rp145.000,-</td></tr>
                    <tr><td>Baju muslimah</td><td class="price">Rp145.000,-</td></tr>
                    <tr><td>Baju OR tangan pendek</td><td class="price">Rp185.000,-</td></tr>
                    <tr><td>Baju OR tangan panjang</td><td class="price">Rp195.000,-</td></tr>
                    <tr><td>Topi</td><td class="price">Rp45.000,-</td></tr>
                    <tr><td>Dasi</td><td class="price">Rp45.000,-</td></tr>
                    <tr><td>Ikat pinggang</td><td class="price">Rp140.000,-</td></tr>
                    <tr><td>Jas lab</td><td class="price">Rp140.000,-</td></tr>
                    <tr><td>Rompi</td><td class="price">Rp150.000,-</td></tr>
                  </tbody>
                </table>
              </div>
            </div>
          </div>
        </article>
        <article class="card">
          <h3>Snack & Minuman Sehat</h3>
          <p>Snack bergizi dan minuman sehat tersedia di kantin koperasi.</p>
        </article>
      </div>
    </section>

    <section id="anggota" class="section section-alt">
      <h2>Informasi Anggota</h2>
      <p>Koperasi terdiri dari siswa, guru, dan staf. Keuntungan dibagikan melalui sistem SHU (Sisa Hasil Usaha).</p>
      <p><strong>Jumlah Anggota Aktif:</strong> 717 siswa dan 37 guru</p><br>
      <h2>Struktur Anggota Koperasi :</h2><strong>Ketua :</strong> Rachmat A Syukur, S.Pd.<br><strong>Sekretaris :</strong> Yulianti<br><strong>Bendahara :</strong> Yunita Noor Alfiyah, S.Pd.<br><strong>Bagian Usaha :</strong><br>1. Neneng Fatimah, M.Pd.<br>2. Yuniati Azkia, S.Kom.<br>3. Devi Nurdiani, S.Pd.<br><strong>BPK :</strong><br>1. Asfiah<br>2. Meto Firmansyah, S.Kom</p>



    </section>

    <section id="kontak" class="section">
      <h2>Kontak</h2>
      <div class="contact-list">
        <p>📍 Alamat: Jl. SMA Negeri 103, Jakarta Timur</p>
        <p>📞 Telepon: (021) 123-4567</p>
        <p>✉️ Email: koperasi@sman103.sch.id</p>
      </div>
    </section>
  </main>

  <footer class="site-footer">
    <p>©️ <span id="year"></span> Koperasi SMAN 103 Jakarta. All rights reserved.</p>
  </footer>

  <script>
    // navigasi antar-section menggunakan hash + history (gabungan)
    const links = document.querySelectorAll('a[data-target]');
    const sections = document.querySelectorAll('main .section');
    function showSection(id, push = true){
      sections.forEach(s => s.classList.toggle('active', s.id === id));
      links.forEach(a => a.classList.toggle('active', a.dataset.target === id));
      if(push) history.pushState({section:id}, '', '#' + id);
    }

    links.forEach(a => {
      a.addEventListener('click', e => {
        const target = a.dataset.target;
        if(!target) return;
        e.preventDefault();
        showSection(target);
        window.scrollTo({top:0,behavior:'smooth'});
      });
    });

    window.addEventListener('popstate', e => {
      const id = (e.state && e.state.section) || location.hash.replace('#','') || 'tentang';
      showSection(id, false);
    });

    document.addEventListener('DOMContentLoaded', () => {
      document.getElementById('year').textContent = new Date().getFullYear();
      const initial = location.hash.replace('#','') || 'tentang';
      history.replaceState({section:initial}, '', '#' + initial);
      showSection(initial, false);

      // preload local header image; fallback to remote if missing
      const headerEl = document.querySelector('.site-header');
      const img = new Image();
      img.src = 'images/header.jpg';
      img.onerror = () => headerEl.classList.add('fallback');
    });
  </script>
  <!-- Modal popup for product details -->
  <div class="modal-overlay" id="productModal" role="dialog" aria-hidden="true" aria-label="Detail produk">
    <div class="modal" role="document">
      <div class="modal-header">
        <h3 id="modalTitle">Detail Produk</h3>
        <div>
          <button class="modal-close" id="modalClose" aria-label="Tutup">✕</button>
        </div>
      </div>
      <div class="modal-body" id="modalBody">
        <!-- injected content -->
      </div>
    </div>
  </div>
  <script>
    // Toggle details for product buttons (Alat Tulis, Seragam, etc.)
    document.addEventListener('DOMContentLoaded', () => {
      const buttons = document.querySelectorAll('.product-btn');
      buttons.forEach(btn => {
        const panelId = btn.getAttribute('aria-controls');
        const panel = document.getElementById(panelId);
        if(!panel) return;
        btn.addEventListener('click', () => {
          const showing = panel.classList.toggle('show');
          panel.setAttribute('aria-hidden', String(!showing));
          btn.setAttribute('aria-expanded', String(showing));
          if(showing){
            panel.scrollIntoView({behavior:'smooth', block:'nearest'});
          }
        });
      });
    });
  </script>
</body>
</html>
