<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>WNI & CO. | PARIS HAUTE COUTURE</title>
    <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:wght@300;400;500&family=Montserrat:wght@100;200;300;400&display=swap" rel="stylesheet">
    <style>
        :root { --white: #ffffff; --black: #111111; --silk-blue: #f1f6ff; --gold: #c5a059; }
        * { margin: 0; padding: 0; box-sizing: border-box; outline: none; }
        body { font-family: 'Montserrat', sans-serif; background: var(--silk-blue); color: var(--black); overflow-x: hidden; }

        /* --- HEADER --- */
        header {
            background: var(--white); padding: 15px 4%;
            display: flex; align-items: center; justify-content: space-between;
            position: sticky; top: 0; z-index: 2000; border-bottom: 1px solid #eee;
        }
        .logo-box { font-family: 'Cormorant Garamond', serif; font-size: 24px; font-weight: 500; letter-spacing: 5px; }
        .main-nav { display: flex; gap: 20px; list-style: none; }
        .main-nav a { text-decoration: none; color: var(--black); font-size: 11px; font-weight: 400; letter-spacing: 1px; text-transform: uppercase; }
        .header-right { display: flex; align-items: center; gap: 15px; }
        
        .lang-select { border: 1px solid #eee; background: white; padding: 5px 10px; font-size: 11px; cursor: pointer; border-radius: 4px; }
        .cart-status { font-size: 11px; font-weight: 500; color: var(--gold); }

        /* --- PRODUCT GRID --- */
        .container { padding: 60px 4%; min-height: 80vh; }
        .cat-title { font-family: 'Cormorant Garamond', serif; font-size: 32px; text-align: center; margin-bottom: 50px; letter-spacing: 8px; font-weight: 300; }
        .grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 40px; }

        .card { background: white; padding: 10px; transition: 0.4s; cursor: pointer; border: 1px solid transparent; }
        .card:hover { transform: translateY(-5px); box-shadow: 0 10px 30px rgba(0,0,0,0.05); }
        .img-wrap { height: 450px; overflow: hidden; margin-bottom: 20px; background: #fdfdfd; display: flex; align-items: center; justify-content: center; }
        .img-wrap img { width: 100%; height: 100%; object-fit: cover; }
        .card-info { text-align: center; padding: 10px; }
        .card-info h3 { font-size: 11px; letter-spacing: 2px; font-weight: 400; margin-bottom: 8px; }
        .card-info p { color: var(--gold); font-size: 13px; font-weight: 500; }

        /* --- MODAL --- */
        .modal { position: fixed; inset: 0; background: rgba(0,0,0,0.85); display: none; align-items: center; justify-content: center; z-index: 3000; padding: 20px; }
        .modal-content { background: white; width: 900px; max-width: 100%; display: grid; grid-template-columns: 1fr 1fr; position: relative; border-radius: 2px; }
        .close-btn { position: absolute; top: 15px; right: 20px; cursor: pointer; font-size: 20px; z-index: 10; color: #555; }
        .modal-left img { width: 100%; height: 100%; object-fit: cover; display: block; min-height: 500px; }
        .modal-right { padding: 40px; display: flex; flex-direction: column; gap: 15px; overflow-y: auto; max-height: 90vh; }
        .modal-right h2 { font-family: 'Cormorant Garamond', serif; letter-spacing: 2px; font-size: 20px; margin-bottom: 10px; border-bottom: 1px solid #eee; padding-bottom: 10px; }

        .opt-group label { font-size: 10px; font-weight: 600; letter-spacing: 1px; display: block; margin-bottom: 8px; text-transform: uppercase; }
        .chips { display: flex; gap: 8px; flex-wrap: wrap; margin-bottom: 5px; }
        .chip { border: 1px solid #ddd; padding: 8px 12px; font-size: 10px; cursor: pointer; transition: 0.2s; }
        .chip.active { background: black; color: white; border-color: black; }

        .form-info { background: #f9f9f9; padding: 20px; margin-top: 10px; border: 1px solid #eee; }
        .form-info input { width: 100%; padding: 12px; border: 1px solid #ddd; font-family: 'Montserrat'; font-size: 11px; margin-bottom: 10px; background: white; }
        .form-info input:focus { border-color: var(--gold); }
        
        .btn-add-cart { background: black; color: white; border: none; padding: 18px; font-size: 11px; letter-spacing: 2px; cursor: pointer; margin-top: 10px; transition: 0.3s; font-weight: 600; }
        .btn-add-cart:hover { background: var(--gold); }

        footer { background: #fff; padding: 60px 4%; border-top: 1px solid #eee; margin-top: 100px; }
        .footer-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 40px; }
        .footer-col h4 { font-size: 11px; letter-spacing: 2px; margin-bottom: 20px; color: var(--gold); }
        .footer-col p { font-size: 11px; color: #888; margin-bottom: 10px; font-weight: 200; }
    </style>
</head>
<body>

<header>
    <div class="logo-box">W N I</div>
    <ul class="main-nav">
        <li><a href="javascript:void(0)" onclick="render('Xuan')" id="nav-xuan">SẢN PHẨM MỚI</a></li>
        <li><a href="javascript:void(0)" onclick="render('Giay')" id="nav-giay">GIÀY</a></li>
        <li><a href="javascript:void(0)" onclick="render('Ao')" id="nav-ao">ÁO</a></li>
        <li><a href="javascript:void(0)" onclick="render('Vay')" id="nav-vay">VÁY</a></li>
        <li><a href="javascript:void(0)" onclick="render('Phukien')" id="nav-phu">PHỤ KIỆN</a></li>
    </ul>

    <div class="header-right">
        <select class="lang-select" id="lang-picker" onchange="updateLanguage()">
            <option value="vi">Tiếng Việt</option>
            <option value="en">English</option>
            <option value="kr">한국어</option>
        </select>
        <span class="cart-status" id="txt-cart">👜 0</span>
    </div>
</header>

<div class="container">
    <h2 class="cat-title" id="displayTitle">PARIS COLLECTION</h2>
    <div class="grid" id="productGrid"></div>
</div>

<div class="modal" id="cartModal">
    <div class="modal-content">
        <span class="close-btn" onclick="closeModal()">✕</span>
        <div class="modal-left"><img src="" id="modal-img"></div>
        <div class="modal-right">
            <h2 id="modal-title">PRODUCT CODE</h2>
            
            <div class="opt-group">
                <label id="lbl-color">MÀU SẮC</label>
                <div class="chips" id="color-container">
                    <div class="chip active" onclick="selectChip(this)">NOIR</div>
                    <div class="chip" onclick="selectChip(this)">BLANC</div>
                    <div class="chip" onclick="selectChip(this)">GOLD</div>
                </div>
            </div>

            <div class="opt-group">
                <label id="lbl-size">KÍCH THƯỚC</label>
                <div class="chips" id="size-container">
                    <div class="chip" onclick="selectChip(this)">FR 34</div>
                    <div class="chip active" onclick="selectChip(this)">FR 36</div>
                    <div class="chip" onclick="selectChip(this)">FR 38</div>
                </div>
            </div>

            <div class="form-info">
                <label id="lbl-info">THÔNG TIN GIAO HÀNG</label>
                <input type="text" id="ipt-name" placeholder="Họ và tên khách hàng">
                <input type="text" id="ipt-phone" placeholder="Số điện thoại liên lạc">
                <input type="text" id="ipt-address" placeholder="Địa chỉ nhận hàng tại Việt Nam/Quốc tế">
            </div>

            <button class="btn-add-cart" id="btn-add" onclick="addToCart()">HOÀN TẤT ĐẶT HÀNG</button>
        </div>
    </div>
</div>

<footer>
    <div class="footer-grid">
        <div class="footer-col"><h4 id="f-contact">LIÊN HỆ</h4><p>Hotline: 0876574252</p><p>Email: nguyenhoaithanh959@gmail.com</p></div>
        <div class="footer-col"><h4 id="f-social">FOLLOW US</h4><p>Instagram @wni.ly</p><p>TikTok @wni.ly</p></div>
        <div class="footer-col"><h4 id="f-service">DỊCH VỤ</h4><p>Tư vấn Size 24/7</p><p>Chính sách Haute Couture</p></div>
    </div>
</footer>

<script>
    let cartCount = 0;
    let currentProduct = {};

    const imageLibrary = {
        Xuan: [
            "https://images.unsplash.com/photo-1539109132314-34a9c655304b?w=600",
            "https://images.unsplash.com/photo-1515886657613-9f3515b0c78f?w=600",
            "https://images.unsplash.com/photo-1496747611176-843222e1e57c?w=600",
            "https://images.unsplash.com/photo-1509631179647-0177331693ae?w=600",
            "https://images.unsplash.com/photo-1490481651871-ab68de25d43d?w=600",
            "https://images.unsplash.com/photo-1512436991641-6745cdb1723f?w=600",
            "https://images.unsplash.com/photo-1520975954732-3cdd222995ad?w=600",
            "https://images.unsplash.com/photo-1475184636916-d2bb99620b21?w=600",
            "https://images.unsplash.com/photo-1485968579580-b6d095142e6e?w=600"
        ],
        Giay: [
            "https://images.unsplash.com/photo-1560769629-975ec94e6a86?w=600",
            "https://images.unsplash.com/photo-1543163521-1bf539c55dd2?w=600",
            "https://images.unsplash.com/photo-1535043934128-cf0b28d52f95?w=600",
            "https://images.unsplash.com/photo-1515347619252-60a4bdad8880?w=600",
            "https://images.unsplash.com/photo-1519415943484-9fa1873496d4?w=600",
            "https://images.unsplash.com/photo-1549298916-b41d501d3772?w=600",
            "https://images.unsplash.com/photo-1595950653106-6c9ebd614d3a?w=600",
            "https://images.unsplash.com/photo-1512374382149-233c42b6a83b?w=600",
            "https://images.unsplash.com/photo-1460353581641-37baddab0fa2?w=600"
        ],
        Ao: [
            "https://images.unsplash.com/photo-1551163943-3f6a855d1153?w=600",
            "https://images.unsplash.com/photo-1596755094514-f87e34085b2c?w=600",
            "https://images.unsplash.com/photo-1434389677669-e08b4cac3105?w=600",
            "https://images.unsplash.com/photo-1589156229687-496a31ad1d1f?w=600",
            "https://images.unsplash.com/photo-1564859228273-274232fdb516?w=600",
            "https://images.unsplash.com/photo-1571513722275-4b41940f54b8?w=600",
            "https://images.unsplash.com/photo-1554568218-0f1715e72254?w=600",
            "https://images.unsplash.com/photo-1583743814966-8936f5b7be7a?w=600",
            "https://images.unsplash.com/photo-1467043237213-65f2da53396f?w=600"
        ],
        Vay: [
            "https://images.unsplash.com/photo-1595777457583-95e059d581b8?w=600",
            "https://images.unsplash.com/photo-1572804013309-59a88b7e92f1?w=600",
            "https://images.unsplash.com/photo-1515378791036-0648a3ef77b2?w=600",
            "https://images.unsplash.com/photo-1518831959646-742c3a14ebf7?w=600",
            "https://images.unsplash.com/photo-1502716119720-b23a93e5fe1b?w=600",
            "https://images.unsplash.com/photo-1566174053879-31528523f8ae?w=600",
            "https://images.unsplash.com/photo-1539008835154-333391d224d1?w=600",
            "https://images.unsplash.com/photo-1505022610485-0249ba5b3675?w=600",
            "https://images.unsplash.com/photo-1542596594-649edbc13630?w=600"
        ],
        Phukien: [
            "https://images.unsplash.com/photo-1584917033904-7911ecf56113?w=600",
            "https://images.unsplash.com/photo-1548036328-c9fa89d128fa?w=600",
            "https://images.unsplash.com/photo-1566150905458-1bf1fd113f0d?w=600",
            "https://images.unsplash.com/photo-1515562141207-7a88fb7ce338?w=600",
            "https://images.unsplash.com/photo-1535632066927-ab7c9ab60908?w=600",
            "https://images.unsplash.com/photo-1599643478518-a784e5dc4c8f?w=600",
            "https://images.unsplash.com/photo-1509112756314-34a0bcb913a3?w=600",
            "https://images.unsplash.com/photo-1511406384665-270e27b19cae?w=600",
            "https://images.unsplash.com/photo-1523170335258-f5ed11844a49?w=600"
        ]
    };

    const translations = {
        vi: { nav: ["SẢN PHẨM MỚI", "GIÀY", "ÁO", "VÁY", "PHỤ KIỆN"], color: "MÀU SẮC", size: "KÍCH THƯỚC", info: "THÔNG TIN GIAO HÀNG", place: ["Họ tên khách hàng", "Số điện thoại", "Địa chỉ nhận hàng"], add: "HOÀN TẤT ĐẶT HÀNG" },
        en: { nav: ["NEW ARRIVALS", "SHOES", "TOPS", "DRESSES", "ACCESSORIES"], color: "COLORS", size: "SIZES", info: "SHIPPING INFORMATION", place: ["Customer Name", "Phone Number", "Delivery Address"], add: "COMPLETE ORDER" },
        kr: { nav: ["신상품", "신발", "상의", "드레스", "액세서리"], color: "색상", size: "사이즈", info: "배송 정보", place: ["고객 성함", "전화번호", "배송 주소"], add: "주문 완료" }
    };

    function updateLanguage() {
        const lang = document.getElementById('lang-picker').value;
        const t = translations[lang];
        document.getElementById('nav-xuan').innerText = t.nav[0];
        document.getElementById('nav-giay').innerText = t.nav[1];
        document.getElementById('nav-ao').innerText = t.nav[2];
        document.getElementById('nav-vay').innerText = t.nav[3];
        document.getElementById('nav-phu').innerText = t.nav[4];
        document.getElementById('lbl-color').innerText = t.color;
        document.getElementById('lbl-size').innerText = t.size;
        document.getElementById('lbl-info').innerText = t.info;
        document.getElementById('ipt-name').placeholder = t.place[0];
        document.getElementById('ipt-phone').placeholder = t.place[1];
        document.getElementById('ipt-address').placeholder = t.place[2];
        document.getElementById('btn-add').innerText = t.add;
        render(document.getElementById('displayTitle').getAttribute('data-cat') || 'Xuan');
    }

    function render(category) {
        const grid = document.getElementById('productGrid');
        const title = document.getElementById('displayTitle');
        grid.innerHTML = '';
        title.innerText = category.toUpperCase() + ' PARIS';
        title.setAttribute('data-cat', category);

        imageLibrary[category].forEach((img, index) => {
            const code = `${category.slice(0,2).toUpperCase()}-${index + 10}`;
            const card = document.createElement('div');
            card.className = 'card';
            card.innerHTML = `
                <div class="img-wrap"><img src="${img}" onerror="this.closest('.card').remove()"></div>
                <div class="card-info">
                    <h3>PARIS CODE: ${code}</h3>
                    <p>${(Math.floor(Math.random()*30)+20).toLocaleString()}.000.000đ</p>
                </div>`;
            card.onclick = () => openModal(img, `PARIS CODE: ${code}`);
            grid.appendChild(card);
        });
    }

    function selectChip(el) {
        const siblings = el.parentElement.querySelectorAll('.chip');
        siblings.forEach(s => s.classList.remove('active'));
        el.classList.add('active');
    }

    function openModal(img, title) {
        currentProduct = { img, title };
        document.getElementById('modal-img').src = img;
        document.getElementById('modal-title').innerText = title;
        document.getElementById('cartModal').style.display = 'flex';
    }

    function closeModal() { document.getElementById('cartModal').style.display = 'none'; }

    function addToCart() {
        const name = document.getElementById('ipt-name').value;
        const phone = document.getElementById('ipt-phone').value;
        const addr = document.getElementById('ipt-address').value;
        const color = document.querySelector('#color-container .chip.active').innerText;
        const size = document.querySelector('#size-container .chip.active').innerText;

        if(!name || !phone || !addr) {
            alert("Vui lòng điền đầy đủ thông tin để chúng tôi có thể xử lý đơn hàng của bạn.");
            return;
        }

        cartCount++;
        document.getElementById('txt-cart').innerText = `👜 ${cartCount}`;
        
        alert(`CHÚC MỪNG!\nĐơn hàng ${currentProduct.title} đã được tiếp nhận.\n\nThông tin đặt hàng:\n- Màu: ${color}\n- Size: ${size}\n- Khách hàng: ${name}\n- SĐT: ${phone}\n- Địa chỉ: ${addr}\n\nChúng tôi sẽ sớm liên hệ với bạn!`);
        
        closeModal();
        // Reset form
        document.getElementById('ipt-name').value = '';
        document.getElementById('ipt-phone').value = '';
        document.getElementById('ipt-address').value = '';
    }

    window.onclick = (e) => { if(e.target == document.getElementById('cartModal')) closeModal(); }
    render('Xuan');
</script>
</body>
</html>
