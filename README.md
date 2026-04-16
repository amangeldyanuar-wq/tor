<!DOCTYPE html>
<html lang="kk">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tör — Фьюжн ресторан</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <script src="https://code.iconify.design/3/3.1.0/iconify.min.js"></script>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Playfair+Display:ital,wght@0,400;0,500;0,600;0,700;1,400&display=swap" rel="stylesheet">
  <script>
    tailwind.config = {
      theme: {
        extend: {
          colors: {
            cream: '#FDFCF8',
            savor: '#F3EFE0',
            gold: '#C9A96E',
            deepred: '#8B2D2D',
            vintage: '#2C1810',
            parchment: '#F5E6C8',
          },
          fontFamily: {
            sans: ['Inter', 'sans-serif'],
            serif: ['Playfair Display', 'serif'],
          },
        }
      }
    }
  </script>
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }
    html { scroll-behavior: smooth; }
    @keyframes fadeInUp {
      from { opacity: 0; transform: translateY(30px); }
      to { opacity: 1; transform: translateY(0); }
    }
    .animate-fade-in-up { animation: fadeInUp 1s cubic-bezier(0.16, 1, 0.3, 1) forwards; }
    .animate-delay-100 { animation-delay: 100ms; }
    .animate-delay-200 { animation-delay: 200ms; }
    .animate-delay-300 { animation-delay: 300ms; }
    .animate-delay-400 { animation-delay: 400ms; }
    .reveal {
      opacity: 0; filter: blur(8px); transform: translateY(24px);
      transition: all 1.2s cubic-bezier(0.16, 1, 0.3, 1);
    }
    .reveal.active { opacity: 1; filter: blur(0); transform: translateY(0); }
    @keyframes pulse-slow { 0%, 100% { transform: scale(1.05); } 50% { transform: scale(1.1); } }
    .animate-pulse-slow { animation: pulse-slow 15s ease-in-out infinite; }
    @keyframes float { 0%, 100% { transform: translateY(0); } 50% { transform: translateY(-10px); } }
    .animate-float { animation: float 6s ease-in-out infinite; }
    @keyframes spin-slow { from { transform: rotate(0deg); } to { transform: rotate(360deg); } }
    .animate-spin-slow { animation: spin-slow 60s linear infinite; }
    .glass-card {
      background: rgba(28, 25, 23, 0.4); backdrop-filter: blur(12px);
      border: 1px solid rgba(255, 255, 255, 0.1); transition: all 500ms ease;
    }
    .glass-card:hover {
      background: rgba(28, 25, 23, 0.6); border-color: rgba(255, 255, 255, 0.2); transform: translateY(-4px);
    }
    .vintage-card {
      background: linear-gradient(145deg, #FDF8EF, #F5E6C8);
      border: 2px solid #C9A96E; position: relative; transition: all 500ms ease;
    }
    .vintage-card:hover { box-shadow: 0 12px 40px rgba(201, 169, 110, 0.25); transform: translateY(-4px); }
    .vintage-card::before {
      content: ''; position: absolute; inset: 6px;
      border: 1px solid rgba(201, 169, 110, 0.4); border-radius: inherit; pointer-events: none;
    }
    .nav-scrolled {
      background: rgba(28, 25, 23, 0.85) !important;
      backdrop-filter: blur(24px) !important; box-shadow: 0 1px 3px rgba(0,0,0,0.2);
    }
    .gold-line { background: linear-gradient(90deg, transparent, #C9A96E, transparent); height: 1px; }
    .text-gradient {
      background: linear-gradient(135deg, #C9A96E, #E8D5A3, #C9A96E);
      -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;
    }
    .vintage-photo { position: relative; overflow: hidden; }
    .vintage-photo::after {
      content: ''; position: absolute; inset: 0;
      background: linear-gradient(180deg, rgba(201,169,110,0.08) 0%, transparent 30%, transparent 70%, rgba(44,24,16,0.12) 100%);
      pointer-events: none; mix-blend-mode: multiply;
    }
    .vintage-photo img { filter: sepia(0.12) contrast(1.05) saturate(0.92); transition: all 700ms ease; }
    .vintage-photo:hover img { filter: sepia(0) contrast(1.08) saturate(1); transform: scale(1.06); }
    .corner-ornament { position: relative; }
    .corner-ornament::before, .corner-ornament::after {
      content: '❧'; position: absolute; color: #C9A96E; font-size: 14px; opacity: 0.6; z-index: 2;
    }
    .corner-ornament::before { top: 8px; left: 12px; }
    .corner-ornament::after { bottom: 8px; right: 12px; transform: rotate(180deg); }
    .ornament-text::before, .ornament-text::after {
      content: '◆'; color: #C9A96E; font-size: 6px; margin: 0 10px; vertical-align: middle;
    }
    .vintage-divider { display: flex; align-items: center; gap: 16px; }
    .vintage-divider::before, .vintage-divider::after {
      content: ''; flex: 1; height: 1px; background: linear-gradient(90deg, transparent, #C9A96E, transparent);
    }
    ::-webkit-scrollbar { width: 8px; }
    ::-webkit-scrollbar-track { background: #1c1917; }
    ::-webkit-scrollbar-thumb { background: #C9A96E; border-radius: 4px; }
    .mobile-menu { transform: translateX(100%); transition: transform 400ms cubic-bezier(0.16, 1, 0.3, 1); }
    .mobile-menu.open { transform: translateX(0); }
    .toast { transform: translateY(100px); opacity: 0; transition: all 400ms cubic-bezier(0.16, 1, 0.3, 1); }
    .toast.show { transform: translateY(0); opacity: 1; }
  </style>
</head>
<body class="font-sans bg-stone-50 text-stone-900 overflow-x-hidden">

  <!-- NAVIGATION -->
  <nav id="navbar" class="fixed top-0 left-0 w-full z-50 transition-all duration-500" style="background: transparent;">
    <div class="max-w-7xl mx-auto px-6 h-20 flex items-center justify-between">
      <a href="#hero" class="flex items-center gap-3">
        <div class="w-10 h-10 rounded-full border-2 border-gold flex items-center justify-center">
          <span class="font-serif text-gold text-lg font-semibold">T</span>
        </div>
        <span class="font-serif text-2xl font-semibold text-cream tracking-wide">Tör</span>
      </a>
      <div class="hidden md:flex items-center gap-8">
        <a href="#about" class="text-cream/70 hover:text-cream text-sm font-medium tracking-wide transition-colors duration-300">Концепция</a>
        <a href="#menu" class="text-cream/70 hover:text-cream text-sm font-medium tracking-wide transition-colors duration-300">Мәзір</a>
        <a href="#drinks" class="text-cream/70 hover:text-cream text-sm font-medium tracking-wide transition-colors duration-300">Сусындар</a>
        <a href="#desserts" class="text-cream/70 hover:text-cream text-sm font-medium tracking-wide transition-colors duration-300">Тәттілер</a>
        <a href="#reserve" class="ml-4 px-6 py-2.5 bg-gold text-stone-900 rounded-full text-sm font-semibold hover:scale-105 transition-transform duration-150">Брондау</a>
      </div>
      <button class="md:hidden text-cream" onclick="toggleMobileMenu()">
        <span class="iconify" data-icon="mdi:menu" data-width="28"></span>
      </button>
    </div>
  </nav>

  <div id="mobileMenu" class="mobile-menu fixed top-0 right-0 w-80 h-full bg-stone-900/95 backdrop-blur-xl z-[60] p-8 flex flex-col">
    <button onclick="toggleMobileMenu()" class="self-end text-cream mb-10">
      <span class="iconify" data-icon="mdi:close" data-width="28"></span>
    </button>
    <div class="flex flex-col gap-6">
      <a href="#about" onclick="toggleMobileMenu()" class="text-cream/80 hover:text-cream text-lg font-medium">Концепция</a>
      <a href="#menu" onclick="toggleMobileMenu()" class="text-cream/80 hover:text-cream text-lg font-medium">Мәзір</a>
      <a href="#drinks" onclick="toggleMobileMenu()" class="text-cream/80 hover:text-cream text-lg font-medium">Сусындар</a>
      <a href="#desserts" onclick="toggleMobileMenu()" class="text-cream/80 hover:text-cream text-lg font-medium">Тәттілер</a>
      <a href="#reserve" onclick="toggleMobileMenu()" class="mt-4 px-6 py-3 bg-gold text-stone-900 rounded-full text-center font-semibold">Брондау</a>
    </div>
  </div>
  <div id="mobileOverlay" class="fixed inset-0 bg-black/50 z-[55] hidden" onclick="toggleMobileMenu()"></div>

  <!-- HERO -->
  <section id="hero" class="relative h-[90vh] flex items-center justify-center overflow-hidden rounded-b-[3rem]">
    <div class="absolute inset-0">
      <img src="https://picsum.photos/seed/tor-restaurant-kz/1920/1080.jpg" alt="Tör Restaurant" class="w-full h-full object-cover animate-pulse-slow scale-105">
      <div class="absolute inset-0 bg-gradient-to-b from-stone-900/70 via-stone-900/50 to-stone-900/80"></div>
    </div>
    <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[600px] h-[600px] border border-gold/10 rounded-full animate-spin-slow pointer-events-none"></div>
    <div class="relative z-10 text-center px-6 max-w-5xl">
      <div class="opacity-0 animate-fade-in-up">
        <p class="text-gold text-xs md:text-sm font-bold tracking-[0.3em] uppercase mb-6">Фьюжн ресторан</p>
      </div>
      <h1 class="opacity-0 animate-fade-in-up animate-delay-100 font-serif text-cream text-5xl md:text-8xl font-medium tracking-tighter leading-[0.85] mb-6">Tör</h1>
      <div class="opacity-0 animate-fade-in-up animate-delay-200">
        <div class="flex items-center justify-center gap-4 mb-8">
          <div class="h-px w-16 bg-gold/50"></div>
          <span class="text-gold/80 text-sm tracking-[0.2em] uppercase">төр</span>
          <div class="h-px w-16 bg-gold/50"></div>
        </div>
      </div>
      <p class="opacity-0 animate-fade-in-up animate-delay-300 text-cream/70 text-lg md:text-xl font-light max-w-2xl mx-auto leading-relaxed mb-10">
        Қазақтың дәстүрлі дәмі мен еуропалық асхананың өнері тоғысқан жерде — Италия мен Францияның нәзіктігі дала рухымен ұялайды
      </p>
      <div class="opacity-0 animate-fade-in-up animate-delay-400 flex flex-col sm:flex-row gap-4 justify-center">
        <a href="#menu" class="px-8 py-4 bg-gold text-stone-900 rounded-full font-semibold text-sm hover:scale-105 transition-transform duration-150">Мәзірді қарау</a>
        <a href="#reserve" class="px-8 py-4 border border-cream/30 text-cream rounded-full font-semibold text-sm hover:bg-cream/10 hover:scale-105 transition-all duration-300">Стол брондау</a>
      </div>
    </div>
    <div class="absolute bottom-8 left-1/2 -translate-x-1/2 animate-float">
      <div class="w-6 h-10 border-2 border-cream/30 rounded-full flex justify-center pt-2">
        <div class="w-1 h-2.5 bg-cream/50 rounded-full"></div>
      </div>
    </div>
  </section>

  <!-- ABOUT -->
  <section id="about" class="py-24 md:py-32 px-6">
    <div class="max-w-7xl mx-auto">
      <div class="flex flex-col lg:flex-row items-center gap-16 lg:gap-20">
        <div class="reveal lg:w-2/5 relative">
          <div class="relative">
            <img src="https://picsum.photos/seed/tor-interior-fusion/600/800.jpg" alt="Tör интерьер" class="rounded-2xl w-full aspect-[3/4] object-cover grayscale-[20%] hover:grayscale-0 transition-all duration-700">
            <div class="absolute -bottom-4 -right-4 bg-gold text-stone-900 px-6 py-3 rounded-xl font-serif text-lg font-semibold shadow-xl">Est. 2024</div>
          </div>
        </div>
        <div class="reveal lg:w-3/5">
          <p class="text-gold text-xs font-bold tracking-[0.3em] uppercase mb-4">Біздің концепция</p>
          <h2 class="font-serif text-4xl md:text-6xl font-medium tracking-tighter leading-[0.85] mb-8">Дала рухы мен<br><span class="text-gradient">Еуропа өнері</span></h2>
          <div class="gold-line w-20 mb-8"></div>
          <p class="text-stone-500 text-lg leading-relaxed mb-6">«Tör» — қазақтың қонақжайлық дәстүрі мен еуропалық гастрономияның жетістіктерін біріктіретін фьюжн ресторан. Біздің асханада бешбармақ лазанья болып қайта туылады, қазы раволи формасын алады, ал дала тағамдары итальян және француз техникерлерімен жаңа өмірге келеді.</p>
          <p class="text-stone-500 text-lg leading-relaxed mb-10">«Төр» — қазақ үйіндегі ең құрметті орын. Біз сізді сол құрметпен қарсы аламыз.</p>
          <div class="grid grid-cols-3 gap-6">
            <div class="text-center"><p class="font-serif text-3xl md:text-4xl text-gradient font-semibold">3</p><p class="text-stone-400 text-sm mt-1">Асхана дәстүрі</p></div>
            <div class="text-center"><p class="font-serif text-3xl md:text-4xl text-gradient font-semibold">12+</p><p class="text-stone-400 text-sm mt-1">Фьюжн тағам</p></div>
            <div class="text-center"><p class="font-serif text-3xl md:text-4xl text-gradient font-semibold">∞</p><p class="text-stone-400 text-sm mt-1">Қонақжайлық</p></div>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- MAIN MENU -->
  <section id="menu" class="py-24 md:py-32 px-6 rounded-t-[3rem]" style="background: linear-gradient(180deg, #1c1917 0%, #2C1810 100%);">
    <div class="max-w-7xl mx-auto">
      <div class="text-center mb-16 reveal">
        <p class="text-gold text-xs font-bold tracking-[0.3em] uppercase mb-4">Бас мәзір</p>
        <h2 class="font-serif text-cream text-4xl md:text-6xl font-medium tracking-tighter leading-[0.85] mb-6">Фьюжн тағамдар</h2>
        <div class="vintage-divider max-w-xs mx-auto">
          <span class="text-gold/60 text-xs tracking-[0.2em] uppercase">Negosýlyq taghamdar</span>
        </div>
      </div>

      <!-- MAIN DISHES -->
      <div class="mb-20">
        <h3 class="reveal text-gold/70 text-sm font-bold tracking-[0.2em] uppercase mb-10 text-center ornament-text">Негізгі тағамдар</h3>
        <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
          <div class="reveal vintage-card corner-ornament rounded-2xl overflow-hidden">
            <div class="vintage-photo h-56 overflow-hidden">
              <img src="https://z-cdn-media.chatglm.cn/files/bd0ab8c1-37d9-4a38-9106-b2bba12fa78e.jpg?auth_key=1876340523-2d8143e4209a4bc59a9c8ee828c2c1e1-0-38d0afecbb5d05b28aa30260aaf3a86b" alt="Qazy Ravioli" class="w-full h-full object-cover object-center">
            </div>
            <div class="p-6 text-center">
              <h4 class="font-serif text-vintage text-xl font-semibold mb-1">Qazy Ravioli</h4>
              <p class="text-gold font-bold text-lg mb-2">6000 ₸</p>
              <p class="text-stone-600 text-sm leading-relaxed">Қазы, рикотта, жұмыртқа қамыры, шөп дәмдеуіштер, пармезан</p>
            </div>
          </div>
          <div class="reveal vintage-card corner-ornament rounded-2xl overflow-hidden">
            <div class="vintage-photo h-56 overflow-hidden">
              <img src="https://z-cdn-media.chatglm.cn/files/a1826381-3a8d-46f5-acab-08695ea5e6a7.jpg?auth_key=1876340523-4fe1a46933b8435ea929af113b7fda35-0-a7e62f6e03a6c4a5d19b8645dbf2b743" alt="Beshbarmak Lasagna" class="w-full h-full object-cover object-center">
            </div>
            <div class="p-6 text-center">
              <h4 class="font-serif text-vintage text-xl font-semibold mb-1">Beshbarmak Lasagna</h4>
              <p class="text-gold font-bold text-lg mb-2">7000 ₸</p>
              <p class="text-stone-600 text-sm leading-relaxed">Қабырта, жылқы еті, бешбармақ қамыры, бешамель соусы, пияз</p>
            </div>
          </div>
          <div class="reveal vintage-card corner-ornament rounded-2xl overflow-hidden">
            <div class="vintage-photo h-56 overflow-hidden">
              <img src="https://z-cdn-media.chatglm.cn/files/d504b026-6e30-4e89-ad63-d67172cbd0cd.jpg?auth_key=1876340523-e2b2570c3495413384a4cac8219b1112-0-d3485d6d5a04ad8eb09ba5659babd0c7" alt="Lamb à la Steppe" class="w-full h-full object-cover object-center">
            </div>
            <div class="p-6 text-center">
              <h4 class="font-serif text-vintage text-xl font-semibold mb-1">Lamb à la Steppe</h4>
              <p class="text-gold font-bold text-lg mb-2">7000 ₸</p>
              <p class="text-stone-600 text-sm leading-relaxed">Қой еті, розмарин, сарымсақ, картоп гратен, жібек шөп соусы</p>
            </div>
          </div>
          <div class="reveal vintage-card corner-ornament rounded-2xl overflow-hidden">
            <div class="vintage-photo h-56 overflow-hidden">
              <img src="https://z-cdn-media.chatglm.cn/files/04fb054f-f0fe-4f6c-b355-4ac5170caf13.jpg?auth_key=1876340523-b1cda16249fb4d5e9d2c9ce8acf2cdd6-0-5e58c5fe0a7cf3ab59c0af0ff4b17a13" alt="Qazy Risotto" class="w-full h-full object-cover object-center">
            </div>
            <div class="p-6 text-center">
              <h4 class="font-serif text-vintage text-xl font-semibold mb-1">Qazy Risotto</h4>
              <p class="text-gold font-bold text-lg mb-2">5500 ₸</p>
              <p class="text-stone-600 text-sm leading-relaxed">Арборио күріші, қазы, ақ шарап, пармезан, сары май</p>
            </div>
          </div>
        </div>
      </div>

      <!-- SALADS -->
      <div>
        <h3 class="reveal text-gold/70 text-sm font-bold tracking-[0.2em] uppercase mb-10 text-center ornament-text">Салаттар</h3>
        <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
          <div class="reveal vintage-card corner-ornament rounded-2xl overflow-hidden">
            <div class="vintage-photo h-48 overflow-hidden">
              <img src="https://z-cdn-media.chatglm.cn/files/b8b8bc96-2b16-4f44-ab2d-097b02798fd2.jpg?auth_key=1876339337-415e6ad0fd6445779452ee235f7563c3-0-d887b3bed791f73f0dcc4ea7635555f2" alt="Caesar" class="w-full h-full object-cover object-center">
            </div>
            <div class="p-5 text-center">
              <h4 class="font-serif text-vintage text-lg font-semibold mb-1">Caesar</h4>
              <p class="text-gold font-bold mb-2">3500 ₸</p>
              <p class="text-stone-600 text-sm leading-relaxed">Стейк, жасыл салат, пармезан, крутон, үй соусы</p>
            </div>
          </div>
          <div class="reveal vintage-card corner-ornament rounded-2xl overflow-hidden">
            <div class="vintage-photo h-48 overflow-hidden">
              <img src="https://z-cdn-media.chatglm.cn/files/0d2220ac-3604-4d1d-be61-7e4eee212439.jpg?auth_key=1876339337-6c95959db0704adf9ade963532c06651-0-d0890dd6cfaaac778534e1c538be2b62" alt="Thai Beef à la Steppe" class="w-full h-full object-cover object-center">
            </div>
            <div class="p-5 text-center">
              <h4 class="font-serif text-vintage text-lg font-semibold mb-1">Thai Beef <span class="italic">à la Steppe</span></h4>
              <p class="text-gold font-bold mb-2">4500 ₸</p>
              <p class="text-stone-600 text-sm leading-relaxed">Жіңішке ет, салат, қияр, лимонграсс, чили, лайм, соя, зәйтүн, кинза</p>
            </div>
          </div>
          <div class="reveal vintage-card corner-ornament rounded-2xl overflow-hidden">
            <div class="vintage-photo h-48 overflow-hidden">
              <img src="https://z-cdn-media.chatglm.cn/files/6c07a765-0f18-4aed-bffa-cbcd10fb960f.jpg?auth_key=1876339337-c8c34b4270564b43a96c65f7ec07b204-0-0fc08028a5718f4699892274603f0694" alt="Greek Salad Dala Style" class="w-full h-full object-cover object-center">
            </div>
            <div class="p-5 text-center">
              <h4 class="font-serif text-vintage text-lg font-semibold mb-1">Greek Salad "Dala Style"</h4>
              <p class="text-gold font-bold mb-2">3000 ₸</p>
              <p class="text-stone-600 text-sm leading-relaxed">Капуста, қияр, бұрыш, пияз, зәйтүн майы, петрушка</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- DRINKS — СУСЫНДАР -->
  <section id="drinks" class="py-24 md:py-32 px-6" style="background: linear-gradient(180deg, #F5E6C8 0%, #F3EFE0 100%);">
    <div class="max-w-7xl mx-auto">
      <div class="text-center mb-16 reveal">
        <p class="text-gold text-xs font-bold tracking-[0.3em] uppercase mb-4">Сусындар</p>
        <h2 class="font-serif text-vintage text-4xl md:text-6xl font-medium tracking-tighter leading-[0.85] mb-6">Сусындар · Шай · Лимонад</h2>
        <div class="vintage-divider max-w-xs mx-auto">
          <span class="text-gold/80 text-xs tracking-[0.2em] uppercase">Syýyndar</span>
        </div>
      </div>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
        <div class="reveal vintage-card corner-ornament rounded-2xl p-8">
          <div class="text-center mb-6">
            <div class="w-16 h-16 mx-auto rounded-full bg-gold/15 flex items-center justify-center mb-4 border border-gold/30">
              <span class="iconify text-gold" data-icon="mdi:cup" data-width="30"></span>
            </div>
            <h3 class="font-serif text-vintage text-2xl font-semibold">Сусындар</h3>
          </div>
          <div class="space-y-4">
            <div class="flex justify-between items-baseline border-b border-gold/20 pb-3"><div><p class="font-medium text-vintage">Қымыз</p><p class="text-stone-500 text-xs">Биенің сүтінен</p></div><span class="text-gold font-bold">2000 ₸</span></div>
            <div class="flex justify-between items-baseline border-b border-gold/20 pb-3"><div><p class="font-medium text-vintage">Шұбат</p><p class="text-stone-500 text-xs">Түйенің сүтінен</p></div><span class="text-gold font-bold">2000 ₸</span></div>
            <div class="flex justify-between items-baseline"><div><p class="font-medium text-vintage">Айран</p><p class="text-stone-500 text-xs">Сүт, қатық</p></div><span class="text-gold font-bold">1000 ₸</span></div>
          </div>
        </div>
        <div class="reveal vintage-card corner-ornament rounded-2xl p-8">
          <div class="text-center mb-6">
            <div class="w-16 h-16 mx-auto rounded-full bg-gold/15 flex items-center justify-center mb-4 border border-gold/30">
              <span class="iconify text-gold" data-icon="mdi:tea" data-width="30"></span>
            </div>
            <h3 class="font-serif text-vintage text-2xl font-semibold">Шай</h3>
          </div>
          <div class="space-y-4">
            <div class="flex justify-between items-baseline border-b border-gold/20 pb-3"><div><p class="font-medium text-vintage">Алматы шай</p><p class="text-stone-500 text-xs">Жасыл шай, лимон, бал</p></div><span class="text-gold font-bold">1500 ₸</span></div>
            <div class="flex justify-between items-baseline border-b border-gold/20 pb-3"><div><p class="font-medium text-vintage">Ташкент шай</p><p class="text-stone-500 text-xs">Қара шай, дәмдеуіштер</p></div><span class="text-gold font-bold">1000 ₸</span></div>
            <div class="flex justify-between items-baseline"><div><p class="font-medium text-vintage">Дала шай</p><p class="text-stone-500 text-xs">Жантақ, шайқурай</p></div><span class="text-gold font-bold">1200 ₸</span></div>
          </div>
        </div>
        <div class="reveal vintage-card corner-ornament rounded-2xl p-8">
          <div class="text-center mb-6">
            <div class="w-16 h-16 mx-auto rounded-full bg-gold/15 flex items-center justify-center mb-4 border border-gold/30">
              <span class="iconify text-gold" data-icon="mdi:glass-cocktail" data-width="30"></span>
            </div>
            <h3 class="font-serif text-vintage text-2xl font-semibold">Лимонад</h3>
          </div>
          <div class="space-y-4">
            <div class="flex justify-between items-baseline border-b border-gold/20 pb-3"><div><p class="font-medium text-vintage">Мохито</p><p class="text-stone-500 text-xs">Жасыл лимон, мята, содовая</p></div><span class="text-gold font-bold">3000 ₸</span></div>
            <div class="flex justify-between items-baseline border-b border-gold/20 pb-3"><div><p class="font-medium text-vintage">Қарақат лимонад</p><p class="text-stone-500 text-xs">Қарақат, лайм, бал</p></div><span class="text-gold font-bold">2500 ₸</span></div>
            <div class="flex justify-between items-baseline"><div><p class="font-medium text-vintage">Алма лимонад</p><p class="text-stone-500 text-xs">Алма, имбирь, розмарин</p></div><span class="text-gold font-bold">2500 ₸</span></div>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- DESSERTS -->
  <section id="desserts" class="py-24 md:py-32 px-6 bg-stone-50">
    <div class="max-w-7xl mx-auto">
      <div class="text-center mb-16 reveal">
        <p class="text-gold text-xs font-bold tracking-[0.3em] uppercase mb-4">Тәттілер</p>
        <h2 class="font-serif text-stone-900 text-4xl md:text-6xl font-medium tracking-tighter leading-[0.85] mb-6">Tattiler</h2>
        <div class="vintage-divider max-w-xs mx-auto">
          <span class="text-gold/80 text-xs tracking-[0.2em] uppercase">Дәстүр мен өнер</span>
        </div>
      </div>
      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-8">
        <div class="reveal vintage-card corner-ornament rounded-2xl overflow-hidden">
          <div class="vintage-photo h-52 overflow-hidden">
            <img src="https://z-cdn-media.chatglm.cn/files/2367fcce-0220-4d51-87b3-c0f02943efff.jpg?auth_key=1876337565-2798d1b33b5542948a869b835aaebd19-0-689f95a6454c8b8a545365b4c0b10843" alt="Baýrsag with Cream" class="w-full h-full object-cover object-center">
          </div>
          <div class="p-5 text-center">
            <h4 class="font-serif text-vintage text-lg font-semibold mb-1">Baýrsag with Cream</h4>
            <p class="text-gold font-bold mb-2">1500 ₸</p>
            <p class="text-stone-600 text-sm leading-relaxed">Бауырсақ, крем, ваниль, жидек</p>
          </div>
        </div>
        <div class="reveal vintage-card corner-ornament rounded-2xl overflow-hidden">
          <div class="vintage-photo h-52 overflow-hidden">
            <img src="https://z-cdn-media.chatglm.cn/files/c0a0a12b-a967-421f-811f-ebf32869891f.jpg?auth_key=1876338692-1cc90dad97284364bb3acab9f1da3384-0-c9274bafbd57bf797280dc8ab6493a9a" alt="Jent Cheesecake" class="w-full h-full object-cover object-center">
          </div>
          <div class="p-5 text-center">
            <h4 class="font-serif text-vintage text-lg font-semibold mb-1">Jent Cheesecake</h4>
            <p class="text-gold font-bold mb-2">2500 ₸</p>
            <p class="text-stone-600 text-sm leading-relaxed">Жент, крем-сыр, бал, жидек</p>
          </div>
        </div>
        <div class="reveal vintage-card corner-ornament rounded-2xl overflow-hidden">
          <div class="vintage-photo h-52 overflow-hidden">
            <img src="https://z-cdn-media.chatglm.cn/files/d56d5914-0f37-43a5-b35c-9f83d37a7eac.jpg?auth_key=1876338692-5f2bf7476b274b59a9f3cad6ecad4a5f-0-2cdcaff51cbdb3696aa5e6269c90dece" alt="Irimshik in Chocolate" class="w-full h-full object-cover object-center">
          </div>
          <div class="p-5 text-center">
            <h4 class="font-serif text-vintage text-lg font-semibold mb-1">Irimshik in Chocolate</h4>
            <p class="text-gold font-bold mb-2">2000 ₸</p>
            <p class="text-stone-600 text-sm leading-relaxed">Ірімшік, қара шоколад, жаңғақ, жидек</p>
          </div>
        </div>
        <div class="reveal vintage-card corner-ornament rounded-2xl overflow-hidden">
          <div class="vintage-photo h-52 overflow-hidden">
            <img src="https://z-cdn-media.chatglm.cn/files/f2d6caec-181f-44ef-bbb4-04d04ecc31cf.jpg?auth_key=1876338692-8f762590e11f464f897d497fbc85e4a2-0-e9e3f3c57ca1e5da13efa22f97f503b9" alt="Jent Tiramisu" class="w-full h-full object-cover object-center">
          </div>
          <div class="p-5 text-center">
            <h4 class="font-serif text-vintage text-lg font-semibold mb-1">Jent Tiramisu</h4>
            <p class="text-gold font-bold mb-2">2500 ₸</p>
            <p class="text-stone-600 text-sm leading-relaxed">Жент, маскарпоне, эспрессо, какао</p>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- GALLERY — Real Photos -->
  <section class="py-24 md:py-32 px-6 bg-stone-900 rounded-t-[3rem]">
    <div class="max-w-7xl mx-auto">
      <div class="text-center mb-16 reveal">
        <p class="text-gold text-xs font-bold tracking-[0.3em] uppercase mb-4">Атмосфера</p>
        <h2 class="font-serif text-cream text-4xl md:text-6xl font-medium tracking-tighter leading-[0.85] mb-6">Ресторан көрінісі</h2>
      </div>

      <!-- Main large photo — Interior with chandelier -->
      <div class="reveal rounded-3xl overflow-hidden vintage-photo mb-4">
        <img src="https://z-cdn-media.chatglm.cn/files/c957b055-b062-412a-a9a6-b7e7b6fbb570.jpg?auth_key=1876341332-ef57c31ac13e4d87aec89c7d1f7c5875-0-f41f88c368741d19428aff969244e81a" alt="Tör залы" class="w-full h-[400px] md:h-[500px] object-cover">
      </div>

      <!-- Grid with 4 photos -->
      <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
        <!-- Multi-scene: interior, outdoor, dishes -->
        <div class="reveal rounded-3xl overflow-hidden vintage-photo">
          <img src="https://z-cdn-media.chatglm.cn/files/2de3f21a-eee7-4e2a-b29e-f287523473b8.jpg?auth_key=1876341332-965c1619651f42419d183069ed836677-0-bf573efcbd13d0ba6ee821638888d2ce" alt="Tör көріністер" class="w-full h-64 md:h-80 object-cover">
        </div>
        <!-- Night exterior with TOR sign -->
        <div class="reveal rounded-3xl overflow-hidden vintage-photo">
          <img src="https://z-cdn-media.chatglm.cn/files/f0496d0f-7fd4-41e7-bbe0-2ff08f6f09cf.jpg?auth_key=1876341332-5cd36eccba5247788bfe74e7e7d95a5e-0-28152354cf450307649cf44cfa8239a6" alt="Tör сырты" class="w-full h-64 md:h-80 object-cover">
        </div>
        <!-- Interior private rooms & dishes -->
        <div class="reveal rounded-3xl overflow-hidden vintage-photo">
          <img src="https://z-cdn-media.chatglm.cn/files/cb3e3297-9b50-4409-8136-f7d3c6ab4b77.jpg?auth_key=1876341332-3145f0cd610e41b09e45b46cf8302c33-0-36dd0d01947de606012d7b5304bfd685" alt="Tör жеке бөлме" class="w-full h-64 md:h-80 object-cover">
        </div>
        <!-- Food, interior, sign -->
        <div class="reveal rounded-3xl overflow-hidden vintage-photo">
          <img src="https://z-cdn-media.chatglm.cn/files/a3a1f5fc-ca3e-4b4b-84d7-931cf5adce92.jpg?auth_key=1876341332-324fe596d484445f99b100ef928e7e48-0-0397698405d5cb0a76304a3eb32a09ee" alt="Tör тағамдар" class="w-full h-64 md:h-80 object-cover">
        </div>
      </div>
    </div>
  </section>

  <!-- RESERVATION -->
  <section id="reserve" class="py-24 md:py-32 px-6 bg-stone-900 relative overflow-hidden">
    <div class="absolute top-0 right-0 w-96 h-96 bg-gold/5 rounded-full blur-3xl"></div>
    <div class="absolute bottom-0 left-0 w-72 h-72 bg-deepred/5 rounded-full blur-3xl"></div>
    <div class="max-w-5xl mx-auto relative z-10">
      <div class="flex flex-col lg:flex-row gap-16 items-start">
        <div class="reveal lg:w-2/5">
          <p class="text-gold text-xs font-bold tracking-[0.3em] uppercase mb-4">Брондау</p>
          <h2 class="font-serif text-cream text-4xl md:text-5xl font-medium tracking-tighter leading-[0.85] mb-6">Төрге<br>отырыңыз</h2>
          <div class="gold-line w-20 mb-8"></div>
          <p class="text-stone-400 text-lg leading-relaxed mb-8">Қонақжайлықтың ең жоғары деңгейі — сізді «төрде» күтеміз. Столды алдын ала брондап, ерекше кешні қамтамасыз етіңіз.</p>
          <div class="space-y-4">
            <div class="flex items-center gap-4">
              <div class="w-10 h-10 rounded-full bg-gold/10 flex items-center justify-center"><span class="iconify text-gold" data-icon="mdi:clock-outline" data-width="20"></span></div>
              <div><p class="text-cream text-sm font-medium">Жұмыс уақыты</p><p class="text-stone-500 text-sm">Дүйсенбі — Жексенбі: 12:00 — 00:00</p></div>
            </div>
            <div class="flex items-center gap-4">
              <div class="w-10 h-10 rounded-full bg-gold/10 flex items-center justify-center"><span class="iconify text-gold" data-icon="mdi:phone-outline" data-width="20"></span></div>
              <div><p class="text-cream text-sm font-medium">Телефон</p><p class="text-stone-500 text-sm">+7 (727) 222-33-44</p></div>
            </div>
            <div class="flex items-center gap-4">
              <div class="w-10 h-10 rounded-full bg-gold/10 flex items-center justify-center"><span class="iconify text-gold" data-icon="mdi:map-marker-outline" data-width="20"></span></div>
              <div><p class="text-cream text-sm font-medium">Мекенжай</p><p class="text-stone-500 text-sm">Алматы, Фурманов 52</p></div>
            </div>
          </div>
        </div>
        <div class="reveal lg:w-3/5 w-full">
          <form id="reservationForm" class="glass-card rounded-3xl p-8 md:p-10 space-y-6">
            <div class="grid grid-cols-1 sm:grid-cols-2 gap-6">
              <div>
                <label class="text-cream/60 text-xs font-bold tracking-[0.15em] uppercase block mb-2">Аты-жөні</label>
                <input type="text" required placeholder="Сіздің атыңыз" class="w-full bg-white/5 border border-white/10 rounded-xl px-4 py-3 text-cream placeholder-stone-600 focus:outline-none focus:border-gold/50 transition-colors duration-300">
              </div>
              <div>
                <label class="text-cream/60 text-xs font-bold tracking-[0.15em] uppercase block mb-2">Телефон</label>
                <input type="tel" required placeholder="+7 (___) ___-__-__" class="w-full bg-white/5 border border-white/10 rounded-xl px-4 py-3 text-cream placeholder-stone-600 focus:outline-none focus:border-gold/50 transition-colors duration-300">
              </div>
            </div>
            <div class="grid grid-cols-1 sm:grid-cols-2 gap-6">
              <div>
                <label class="text-cream/60 text-xs font-bold tracking-[0.15em] uppercase block mb-2">Күні</label>
                <input type="date" required class="w-full bg-white/5 border border-white/10 rounded-xl px-4 py-3 text-cream focus:outline-none focus:border-gold/50 transition-colors duration-300 [color-scheme:dark]">
              </div>
              <div>
                <label class="text-cream/60 text-xs font-bold tracking-[0.15em] uppercase block mb-2">Уақыты</label>
                <input type="time" required class="w-full bg-white/5 border border-white/10 rounded-xl px-4 py-3 text-cream focus:outline-none focus:border-gold/50 transition-colors duration-300 [color-scheme:dark]">
              </div>
            </div>
            <div>
              <label class="text-cream/60 text-xs font-bold tracking-[0.15em] uppercase block mb-2">Қонақ саны</label>
              <select required class="w-full bg-white/5 border border-white/10 rounded-xl px-4 py-3 text-cream focus:outline-none focus:border-gold/50 transition-colors duration-300 appearance-none [color-scheme:dark]">
                <option value="" class="bg-stone-800">Таңдаңыз</option>
                <option value="1-2" class="bg-stone-800">1-2 адам</option>
                <option value="3-4" class="bg-stone-800">3-4 адам</option>
                <option value="5-6" class="bg-stone-800">5-6 адам</option>
                <option value="7-10" class="bg-stone-800">7-10 адам</option>
                <option value="10+" class="bg-stone-800">10+ адам</option>
              </select>
            </div>
            <div>
              <label class="text-cream/60 text-xs font-bold tracking-[0.15em] uppercase block mb-2">Арнайы өтініш</label>
              <textarea rows="3" placeholder="Мереке, аллергия, басқа өтініш..." class="w-full bg-white/5 border border-white/10 rounded-xl px-4 py-3 text-cream placeholder-stone-600 focus:outline-none focus:border-gold/50 transition-colors duration-300 resize-none"></textarea>
            </div>
            <button type="submit" class="w-full py-4 bg-gold text-stone-900 rounded-xl font-semibold text-base hover:scale-[1.02] transition-transform duration-150">Брондауды растау</button>
          </form>
        </div>
      </div>
    </div>
  </section>

  <!-- FOOTER -->
  <footer class="bg-stone-950 py-16 px-6 rounded-t-[3rem]">
    <div class="max-w-7xl mx-auto">
      <div class="flex flex-col md:flex-row justify-between items-start gap-12 mb-12">
        <div class="max-w-xs">
          <div class="flex items-center gap-3 mb-4">
            <div class="w-10 h-10 rounded-full border-2 border-gold flex items-center justify-center"><span class="font-serif text-gold text-lg font-semibold">T</span></div>
            <span class="font-serif text-3xl font-semibold text-cream tracking-wide">Tör</span>
          </div>
          <p class="text-stone-500 text-sm leading-relaxed">Қазақ дәмі мен Еуропа өнерінің фьюжн рестораны. Дала рухын әр табақтан сезініңіз.</p>
        </div>
        <div>
          <h4 class="text-cream text-xs font-bold tracking-[0.2em] uppercase mb-4">Мәзір</h4>
          <div class="space-y-2">
            <a href="#menu" class="block text-stone-500 hover:text-cream text-sm transition-colors duration-300">Негізгі тағамдар</a>
            <a href="#menu" class="block text-stone-500 hover:text-cream text-sm transition-colors duration-300">Салаттар</a>
            <a href="#drinks" class="block text-stone-500 hover:text-cream text-sm transition-colors duration-300">Сусындар</a>
            <a href="#desserts" class="block text-stone-500 hover:text-cream text-sm transition-colors duration-300">Тәттілер</a>
          </div>
        </div>
        <div>
          <h4 class="text-cream text-xs font-bold tracking-[0.2em] uppercase mb-4">Байланыс</h4>
          <div class="space-y-2">
            <p class="text-stone-500 text-sm">Алматы, Фурманов 52</p>
            <p class="text-stone-500 text-sm">+7 (727) 222-33-44</p>
            <p class="text-stone-500 text-sm">info@tor-restaurant.kz</p>
          </div>
          <div class="flex gap-3 mt-4">
            <a href="#" class="w-9 h-9 rounded-full bg-white/5 border border-white/10 flex items-center justify-center text-stone-400 hover:text-gold hover:border-gold/30 transition-all duration-300"><span class="iconify" data-icon="mdi:instagram" data-width="18"></span></a>
            <a href="#" class="w-9 h-9 rounded-full bg-white/5 border border-white/10 flex items-center justify-center text-stone-400 hover:text-gold hover:border-gold/30 transition-all duration-300"><span class="iconify" data-icon="mdi:whatsapp" data-width="18"></span></a>
            <a href="#" class="w-9 h-9 rounded-full bg-white/5 border border-white/10 flex items-center justify-center text-stone-400 hover:text-gold hover:border-gold/30 transition-all duration-300"><span class="iconify" data-icon="mdi:telegram" data-width="18"></span></a>
          </div>
        </div>
      </div>
      <div class="gold-line w-full mb-8"></div>
      <div class="flex flex-col md:flex-row justify-between items-center gap-4">
        <p class="text-stone-600 text-xs">© 2024 Tör Restaurant. Барлық құқықтар қорғалған.</p>
        <p class="text-stone-700 text-xs italic font-serif">«Төр — құрметті орын, сыйлы қонаққа арналған»</p>
      </div>
    </div>
  </footer>

  <!-- Toast -->
  <div id="toast" class="toast fixed bottom-8 left-1/2 -translate-x-1/2 z-[70] bg-gold text-stone-900 px-8 py-4 rounded-2xl shadow-2xl font-semibold flex items-center gap-3">
    <span class="iconify" data-icon="mdi:check-circle" data-width="22"></span>
    <span>Брондау сәтті жіберілді!</span>
  </div>

  <script>
    const navbar = document.getElementById('navbar');
    window.addEventListener('scroll', () => {
      navbar.classList.toggle('nav-scrolled', window.scrollY > 50);
    });

    function toggleMobileMenu() {
      const menu = document.getElementById('mobileMenu');
      const overlay = document.getElementById('mobileOverlay');
      menu.classList.toggle('open');
      overlay.classList.toggle('hidden');
      document.body.style.overflow = menu.classList.contains('open') ? 'hidden' : '';
    }

    const revealElements = document.querySelectorAll('.reveal');
    const revealObserver = new IntersectionObserver((entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          const siblings = entry.target.parentElement.querySelectorAll('.reveal');
          let delay = 0;
          siblings.forEach((sib, i) => { if (sib === entry.target) delay = i * 100; });
          setTimeout(() => entry.target.classList.add('active'), delay);
          revealObserver.unobserve(entry.target);
        }
      });
    }, { threshold: 0.1, rootMargin: '0px 0px -50px 0px' });
    revealElements.forEach(el => revealObserver.observe(el));

    document.getElementById('reservationForm').addEventListener('submit', function(e) {
      e.preventDefault();
      const toast = document.getElementById('toast');
      toast.classList.add('show');
      this.reset();
      setTimeout(() => toast.classList.remove('show'), 4000);
    });

    document.querySelectorAll('a[href^="#"]').forEach(anchor => {
      anchor.addEventListener('click', function(e) {
        e.preventDefault();
        const target = document.querySelector(this.getAttribute('href'));
        if (target) target.scrollIntoView({ behavior: 'smooth', block: 'start' });
      });
    });
  </script>
</body>
</html>
