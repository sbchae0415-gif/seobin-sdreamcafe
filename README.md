<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Seobin’s Dream Cafe</title>
    <style>
        /* 기본 스타일 초기화 */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Noto Sans KR', sans-serif;
            background-color: #fdfbf7;
            color: #4a3b32;
            line-height: 1.6;
            overflow-x: hidden;
        }

        /* 헤더 영역 */
        header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 20px 40px;
            background-color: #fff;
            border-bottom: 1px solid #efebe9;
            position: sticky;
            top: 0;
            z-index: 100;
        }

        .logo {
            font-size: 1.5rem;
            font-weight: bold;
            color: #6d4c41;
            letter-spacing: 1px;
        }

        /* 오른쪽 상단 ⋮ 메뉴 버튼 */
        .menu-trigger-btn {
            background: none;
            border: none;
            font-size: 1.8rem;
            cursor: pointer;
            color: #4a3b32;
            padding: 5px 10px;
            border-radius: 4px;
            transition: background 0.2s;
        }

        .menu-trigger-btn:hover {
            background-color: #f5f0eb;
        }

        /* 메인 배너 영역 */
        .hero {
            text-align: center;
            padding: 80px 20px;
            background: linear-gradient(rgba(0,0,0,0.3), rgba(0,0,0,0.3)), url('https://images.unsplash.com/photo-1501339847302-ac426a4a7cbb?auto=format&fit=crop&w=1350&q=80') no-repeat center center/cover;
            color: white;
        }

        .hero h1 {
            font-size: 3rem;
            margin-bottom: 15px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
        }

        .hero p {
            font-size: 1.2rem;
            text-shadow: 1px 1px 2px rgba(0,0,0,0.5);
        }

        /* 카페 소개 및 메뉴 섹션 */
        .container {
            max-width: 1000px;
            margin: 50px auto;
            padding: 0 20px;
        }

        .section-title {
            text-align: center;
            font-size: 2rem;
            margin-bottom: 40px;
            color: #5d4037;
        }

        .menu-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 30px;
        }

        .menu-card {
            background: #fff;
            padding: 25px;
            border-radius: 12px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
            text-align: center;
            transition: transform 0.2s;
        }

        .menu-card:hover {
            transform: translateY(-5px);
        }

        .menu-card h3 {
            margin-bottom: 10px;
            color: #4e342e;
        }

        .menu-card p {
            color: #795548;
            font-size: 0.95rem;
        }

        /* 푸터 */
        footer {
            text-align: center;
            padding: 30px;
            background-color: #efebe9;
            color: #6d4c41;
            margin-top: 80px;
            font-size: 0.9rem;
        }

        /* ================= 사이드 메뉴 (Drawer) 스타일 ================= */
        .sidebar-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.4);
            visibility: hidden;
            opacity: 0;
            transition: opacity 0.3s ease, visibility 0.3s ease;
            z-index: 999;
        }

        .sidebar-overlay.active {
            visibility: visible;
            opacity: 1;
        }

        .sidebar {
            position: fixed;
            top: 0;
            right: -380px;
            width: 380px;
            height: 100%;
            background-color: #fff;
            box-shadow: -4px 0 20px rgba(0,0,0,0.1);
            transition: right 0.35s cubic-bezier(0.16, 1, 0.3, 1);
            z-index: 1000;
            display: flex;
            flex-direction: column;
        }

        .sidebar.active {
            right: 0;
        }

        .sidebar-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 20px 25px;
            border-bottom: 1px solid #eee;
        }

        .sidebar-header h2 {
            font-size: 1.2rem;
            color: #333;
        }

        .sidebar-close-btn {
            background: none;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
            color: #666;
        }

        .sidebar-content {
            padding: 25px;
            overflow-y: auto;
            flex: 1;
        }

        /* 사이드 메뉴 내부의 가상 인스타그램 섹션 */
        .insta-container {
            background-color: #fafafa;
            border: 1px solid #dbdbdb;
            border-radius: 8px;
            padding: 15px;
        }

        .insta-profile-header {
            display: flex;
            align-items: center;
            margin-bottom: 15px;
        }

        .insta-avatar {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            background: linear-gradient(45deg, #f09433, #e6683c, #dc2743, #cc2366, #bc1888);
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: bold;
            font-size: 0.9rem;
            margin-right: 12px;
            flex-shrink: 0;
        }

        .insta-info h4 {
            font-size: 0.95rem;
            color: #262626;
        }

        .insta-info p {
            font-size: 0.8rem;
            color: #8e8e8e;
        }

        .insta-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 6px;
        }

        .insta-post {
            aspect-ratio: 1 / 1;
            background-color: #efefef;
            border-radius: 4px;
            overflow: hidden;
            position: relative;
        }

        .insta-post img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: transform 0.2s;
        }

        .insta-post:hover img {
            transform: scale(1.05);
        }

        /* 반응형 모바일 대응 */
        @media (max-width: 480px) {
            .sidebar {
                width: 100%;
                right: -100%;
            }
        }
    </style>
</head>
<body>

    <!-- 기존 헤더 영역 -->
    <header>
        <div class="logo">☕ Seobin’s Dream Cafe</div>
        <!-- 오른쪽 ⋮ 버튼 -->
        <button class="menu-trigger-btn" id="menuBtn" aria-label="메뉴 열기">⋮</button>
    </header>

    <!-- 기존 메인 배너 영역 -->
    <section class="hero">
        <h1>Welcome to Seobin’s Dream Cafe</h1>
        <p>따뜻한 커피와 포근한 꿈이 머무는 공간입니다.</p>
    </section>

    <!-- 기존 메뉴 소개 영역 -->
    <div class="container">
        <h2 class="section-title">Signature Menu</h2>
        <div class="menu-grid">
            <div class="menu-card">
                <h3>드림 라떼</h3>
                <p>부드러운 크림과 깊은 에스프레소가 조화를 이룬 시그니처 메뉴</p>
            </div>
            <div class="menu-card">
                <h3>바닐라 빈 빈</h3>
                <p>진짜 바닐라 빈을 아낌없이 넣어 달콤하고 향긋한 풍미</p>
            </div>
            <div class="menu-card">
                <h3>초코 포레스트</h3>
                <p>진한 다크 초콜릿의 달콤 쌉싸름함을 느낄 수 있는 음료</p>
            </div>
        </div>
    </div>

    <!-- 기존 푸터 -->
    <footer>
        <p>&copy; 2026 Seobin’s Dream Cafe. All rights reserved.</p>
    </footer>

    <!-- 사이드 메뉴 오버레이 및 패널 -->
    <div class="sidebar-overlay" id="sidebarOverlay"></div>
    <aside class="sidebar" id="sidebar">
        <div class="sidebar-header">
            <h2>Menu & Story</h2>
            <button class="sidebar-close-btn" id="closeBtn">&times;</button>
        </div>
        <div class="sidebar-content">
            <!-- 가상 인스타그램 영역 -->
            <div class="insta-container">
                <div class="insta-profile-header">
                    <div class="insta-avatar">SDC</div>
                    <div class="insta-info">
                        <h4>seobin_dream_cafe</h4>
                        <p>Official Instagram</p>
                    </div>
                </div>
                <div class="insta-grid">
                    <div class="insta-post">
                        <img src="https://images.unsplash.com/photo-1514432324607-a09d9b4aefdd?auto=format&fit=crop&w=300&q=80" alt="카페 사진 1">
                    </div>
                    <div class="insta-post">
                        <img src="https://images.unsplash.com/photo-1495474472287-4d71bcdd2085?auto=format&fit=crop&w=300&q=80" alt="카페 사진 2">
                    </div>
                    <div class="insta-post">
                        <img src="https://images.unsplash.com/photo-1509042239860-f550ce710b93?auto=format&fit=crop&w=300&q=80" alt="카페 사진 3">
                    </div>
                    <div class="insta-post">
                        <img src="https://images.unsplash.com/photo-1447933601403-0c6688de566e?auto=format&fit=crop&w=300&q=80" alt="카페 사진 4">
                    </div>
                    <div class="insta-post">
                        <img src="https://images.unsplash.com/photo-1554118811-1e0d58224f24?auto=format&fit=crop&w=300&q=80" alt="카페 사진 5">
                    </div>
                    <div class="insta-post">
                        <img src="https://images.unsplash.com/photo-1511920170033-f8396924c348?auto=format&fit=crop&w=300&q=80" alt="카페 사진 6">
                    </div>
                </div>
            </div>
        </div>
    </aside>

    <!-- 사이드 메뉴 인터랙션 스크립트 -->
    <script>
        const menuBtn = document.getElementById('menuBtn');
        const closeBtn = document.getElementById('closeBtn');
        const sidebar = document.getElementById('sidebar');
        const sidebarOverlay = document.getElementById('sidebarOverlay');

        function openSidebar() {
            sidebar.classList.add('active');
            sidebarOverlay.classList.add('active');
            document.body.style.overflow = 'hidden'; // 배경 스크롤 방지
        }

        function closeSidebar() {
            sidebar.classList.remove('active');
            sidebarOverlay.classList.remove('active');
            document.body.style.overflow = ''; // 배경 스크롤 복구
        }

        menuBtn.addEventListener('click', openSidebar);
        closeBtn.addEventListener('click', closeSidebar);
        sidebarOverlay.addEventListener('click', closeSidebar);
    </script>
</body>
</html>
