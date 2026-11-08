# Calculator 2006 <!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>เครื่องคิดเงินร้านปริ้นท์อัจฉริยะ (Print Calculator)</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+Thai:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Noto Sans Thai', sans-serif; background-color: #f8fafc; color: #1e293b; scroll-behavior: smooth; -webkit-overflow-scrolling: touch; }
        .dark-mode { background-color: #0f172a; color: #f8fafc; }
        /* Custom smooth scrolling */
        ::-webkit-scrollbar { width: 6px; height: 6px; }
        ::-webkit-scrollbar-track { background: transparent; }
        ::-webkit-scrollbar-thumb { background: rgba(16, 185, 129, 0.2); border-radius: 9999px; }
        ::-webkit-scrollbar-thumb:hover { background: rgba(16, 185, 129, 0.4); }
    </style>
</head>
<body id="mainBody" class="min-h-screen p-4 md:p-8 transition-colors duration-300 dark-mode dark">

    <!-- Top Navigation Header -->
    <header class="max-w-7xl mx-auto bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-800 rounded-3xl p-4 md:p-5 mb-6 flex flex-col md:flex-row justify-between items-center gap-4 shadow-sm">
        <div class="flex items-center gap-3.5">
            <div class="w-12 h-12 bg-emerald-50 dark:bg-emerald-500/10 text-emerald-600 dark:text-emerald-400 rounded-2xl flex items-center justify-center text-xl font-bold border border-emerald-100 dark:border-emerald-500/20">
                <i class="fa-solid fa-print"></i>
            </div>
            <div>
                <div class="flex items-center gap-2">
                    <h1 class="font-bold text-lg text-slate-900 dark:text-white">เครื่องคิดเงินร้านปริ้นท์</h1>
                    <button onclick="openFeaturesModal()" class="bg-emerald-50 hover:bg-emerald-100 dark:bg-emerald-500/20 dark:hover:bg-emerald-500/30 text-emerald-600 dark:text-emerald-400 text-xs px-2.5 py-0.5 rounded-full font-semibold border border-emerald-100 dark:border-emerald-500/30 transition-colors cursor-pointer flex items-center gap-1">
                        Pro v4.6 Midnight Green <i class="fa-solid fa-circle-info text-[10px]"></i>
                    </button>
                </div>
                <p class="text-xs text-slate-500 dark:text-slate-400">ซิงค์ข้อมูลบนคลาวด์และโลคอลอัตโนมัติ (ปลอดภัย 100%)</p>
            </div>
        </div>

        <div class="flex flex-wrap items-center gap-2">
            <button onclick="toggleTheme()" class="bg-slate-100 dark:bg-slate-800 hover:bg-slate-200 dark:hover:bg-slate-700 border border-slate-200 dark:border-slate-700 text-xs px-3.5 py-2.5 rounded-xl text-slate-700 dark:text-slate-300 flex items-center gap-1.5 transition-all font-medium">
                <i id="themeIcon" class="fa-solid fa-sun"></i> <span id="themeLabel">โหมดสว่าง</span>
            </button>
            <button onclick="openPriceModal()" class="bg-slate-100 dark:bg-slate-800 hover:bg-slate-200 dark:hover:bg-slate-700 border border-slate-200 dark:border-slate-700 text-xs px-3.5 py-2.5 rounded-xl text-slate-700 dark:text-slate-300 flex items-center gap-1.5 transition-all font-medium">
                <i class="fa-solid fa-gear"></i> ตั้งค่าราคา
            </button>
            <button onclick="openHistoryModal()" class="bg-slate-100 dark:bg-slate-800 hover:bg-slate-200 dark:hover:bg-slate-700 border border-slate-200 dark:border-slate-700 text-xs px-3.5 py-2.5 rounded-xl text-slate-700 dark:text-slate-300 flex items-center gap-1.5 transition-all font-medium">
                <i class="fa-solid fa-clock-rotate-left"></i> ประวัติการขาย (<span id="historyCount">0</span>)
            </button>
            <button onclick="openCalcModal()" class="bg-indigo-50 dark:bg-indigo-500/10 hover:bg-indigo-100 dark:hover:bg-indigo-500/20 border border-indigo-200 dark:border-indigo-500/20 text-indigo-700 dark:text-indigo-400 text-xs px-3.5 py-2.5 rounded-xl flex items-center gap-1.5 transition-all font-medium">
                <i class="fa-solid fa-calculator"></i> คิดเลขด่วน
            </button>
            <button onclick="openNotesModal()" class="bg-amber-50 dark:bg-amber-500/10 hover:bg-amber-100 border border-amber-200 dark:border-amber-500/20 text-amber-700 dark:text-amber-400 text-xs px-3.5 py-2.5 rounded-xl flex items-center gap-1.5 transition-all font-medium">
                <i class="fa-solid fa-note-sticky"></i> บันทึกข้อความ
            </button>
            <button onclick="openCartModal()" class="bg-emerald-600 hover:bg-emerald-500 text-white text-xs px-4 py-2.5 rounded-xl flex items-center gap-2 font-semibold shadow-lg shadow-emerald-600/20 transition-all">
                <i class="fa-solid fa-cart-shopping"></i> ตะกร้า (<span id="cartCount">0</span>)
            </button>
        </div>
    </header>

    <!-- Main Content Grid -->
    <main class="max-w-7xl mx-auto grid grid-cols-1 lg:grid-cols-3 gap-6">
        
        <!-- Left & Center Panel (Calculator Inputs) -->
        <div class="lg:col-span-2 space-y-6">
            
            <!-- Section 1: Select Print Type -->
            <div class="bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-800 rounded-3xl p-6 shadow-sm space-y-4">
                <div class="flex justify-between items-center mb-2">
                    <div class="flex items-center gap-2.5">
                        <span class="w-7 h-7 rounded-xl bg-emerald-50 dark:bg-emerald-500/20 text-emerald-600 dark:text-emerald-400 border border-emerald-100 dark:border-emerald-500/30 text-xs flex items-center justify-center font-bold">1</span>
                        <h2 class="font-bold text-slate-900 dark:text-white text-base">เลือกประเภทงานพิมพ์</h2>
                    </div>
                </div>

                <div id="printTypesGrid" class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-3.5">
                    <!-- Dynamic Print Types -->
                </div>

                <!-- Custom Price Input Container (Shown when "กำหนดเอง" is selected) -->
                <div id="customPriceContainer" class="hidden bg-emerald-50/50 dark:bg-emerald-950/20 border border-emerald-200 dark:border-emerald-500/30 rounded-2xl p-4 flex flex-col sm:flex-row items-center justify-between gap-3">
                    <div>
                        <h4 class="font-bold text-sm text-emerald-950 dark:text-emerald-200">ระบุราคา 1 ด้าน (กำหนดเอง)</h4>
                        <p class="text-xs text-slate-500 dark:text-slate-400">ระบบจะคำนวณราคา 2 ด้านให้อัตโนมัติ (ลดค่ากระดาษ)</p>
                    </div>
                    <div class="flex items-center gap-2 w-full sm:w-auto">
                        <input type="number" step="0.5" id="mainCustomPriceInput" value="8.00" oninput="updateCustomPrice(this.value)" class="w-full sm:w-32 bg-white dark:bg-slate-900 border border-emerald-300 dark:border-emerald-500/50 rounded-xl px-3 py-2 text-center font-bold text-emerald-600 dark:text-emerald-400 focus:outline-none">
                        <span class="text-xs font-semibold text-slate-600 dark:text-slate-400">บาท/แผ่น</span>
                    </div>
                </div>

                <!-- Section 1.5: Side Selector (1-sided / 2-sided) - Hidden for A4 Plain -->
                <div id="sideSelectorContainer" class="pt-2 border-t border-slate-100 dark:border-slate-800">
                    <div class="flex items-center gap-2 mb-3">
                        <span class="w-6 h-6 rounded-lg bg-emerald-50 dark:bg-emerald-500/20 text-emerald-600 dark:text-emerald-400 text-xs flex items-center justify-center font-bold">1.1</span>
                        <h3 class="font-bold text-slate-900 dark:text-white text-sm">รูปแบบการพิมพ์ (หน้า / หลัง)</h3>
                    </div>
                    <div class="grid grid-cols-2 gap-3.5">
                        <button onclick="setSide(1)" id="side1Btn" class="p-3.5 rounded-2xl border text-center transition-all font-bold text-xs bg-emerald-50 dark:bg-emerald-950/30 border-emerald-500 text-emerald-900 dark:text-white shadow-sm">
                            พิมพ์ 1 ด้าน <span id="side1PriceTag" class="block text-[11px] font-normal text-slate-500 mt-0.5">2.00 ฿ / แผ่น</span>
                        </button>
                        <button onclick="setSide(2)" id="side2Btn" class="p-3.5 rounded-2xl border text-center transition-all font-bold text-xs bg-slate-50 dark:bg-slate-800/40 border-slate-200 dark:border-slate-700 text-slate-600 dark:text-slate-300">
                            พิมพ์ 2 ด้าน <span id="side2PriceTag" class="block text-[11px] font-normal text-slate-500 mt-0.5">3.00 ฿ / แผ่น</span>
                        </button>
                    </div>
                </div>
            </div>

            <!-- Section 2: Copies / Quantity Selector -->
            <div class="bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-800 rounded-3xl p-6 shadow-sm">
                <div class="flex justify-between items-center mb-4">
                    <div class="flex items-center gap-2.5">
                        <span class="w-7 h-7 rounded-xl bg-emerald-50 dark:bg-emerald-500/20 text-emerald-600 dark:text-emerald-400 border border-emerald-100 dark:border-emerald-500/30 text-xs flex items-center justify-center font-bold">2</span>
                        <h2 class="font-bold text-slate-900 dark:text-white text-base">จำนวนแผ่น / สำเนา</h2>
                    </div>
                    <div class="flex bg-slate-100 dark:bg-slate-800 border border-slate-200 dark:border-slate-700 p-1 rounded-2xl text-xs">
                        <button id="modeSliderBtn" onclick="setMode('slider')" class="px-3.5 py-1.5 rounded-xl bg-white dark:bg-emerald-600 text-slate-900 dark:text-white shadow-sm font-semibold transition-all">ตัวเลื่อน</button>
                        <button id="modeInputBtn" onclick="setMode('input')" class="px-3.5 py-1.5 rounded-xl text-slate-500 dark:text-slate-400 font-semibold transition-all">พิมพ์ตัวเลข</button>
                    </div>
                </div>

                <!-- Quantity Display with quick +/- buttons and step buttons -->
                <div class="py-4 text-center flex flex-col items-center justify-center gap-3">
                    <div class="flex items-center justify-center gap-4">
                        <button onclick="adjustQuantity(-1)" class="w-12 h-12 rounded-2xl bg-slate-100 dark:bg-slate-800 hover:bg-slate-200 dark:hover:bg-slate-700 border border-slate-200 dark:border-slate-700 text-slate-700 dark:text-slate-200 flex items-center justify-center text-xl font-bold transition-all shadow-sm">
                            <i class="fa-solid fa-minus"></i>
                        </button>
                        <div>
                            <div id="quantityDisplay" class="text-6xl md:text-7xl font-black text-emerald-600 dark:text-emerald-400 tracking-tight mb-1">1</div>
                            <p class="text-xs text-slate-400 font-medium uppercase tracking-wider">แผ่น</p>
                        </div>
                        <button onclick="adjustQuantity(1)" class="w-12 h-12 rounded-2xl bg-slate-100 dark:bg-slate-800 hover:bg-slate-200 dark:hover:bg-slate-700 border border-slate-200 dark:border-slate-700 text-slate-700 dark:text-slate-200 flex items-center justify-center text-xl font-bold transition-all shadow-sm">
                            <i class="fa-solid fa-plus"></i>
                        </button>
                    </div>

                    <!-- Quick adjustment buttons (-5, -10, -25 / +5, +10, +15) -->
                    <div class="flex flex-wrap items-center justify-center gap-2 pt-2">
                        <button onclick="adjustQuantity(-25)" class="px-3 py-1.5 rounded-xl bg-rose-50 dark:bg-rose-500/10 border border-rose-200 dark:border-rose-500/20 text-rose-600 dark:text-rose-400 text-xs font-bold hover:bg-rose-100">-25</button>
                        <button onclick="adjustQuantity(-10)" class="px-3 py-1.5 rounded-xl bg-rose-50 dark:bg-rose-500/10 border border-rose-200 dark:border-rose-500/20 text-rose-600 dark:text-rose-400 text-xs font-bold hover:bg-rose-100">-10</button>
                        <button onclick="adjustQuantity(-5)" class="px-3 py-1.5 rounded-xl bg-rose-50 dark:bg-rose-500/10 border border-rose-200 dark:border-rose-500/20 text-rose-600 dark:text-rose-400 text-xs font-bold hover:bg-rose-100">-5</button>
                        <div class="h-4 w-[1px] bg-slate-200 dark:bg-slate-700 mx-1"></div>
                        <button onclick="adjustQuantity(5)" class="px-3 py-1.5 rounded-xl bg-emerald-50 dark:bg-emerald-500/10 border border-emerald-200 dark:border-emerald-500/20 text-emerald-600 dark:text-emerald-400 text-xs font-bold hover:bg-emerald-100">+5</button>
                        <button onclick="adjustQuantity(10)" class="px-3 py-1.5 rounded-xl bg-emerald-50 dark:bg-emerald-500/10 border border-emerald-200 dark:border-emerald-500/20 text-emerald-600 dark:text-emerald-400 text-xs font-bold hover:bg-emerald-100">+10</button>
                        <button onclick="adjustQuantity(15)" class="px-3 py-1.5 rounded-xl bg-emerald-50 dark:bg-emerald-500/10 border border-emerald-200 dark:border-emerald-500/20 text-emerald-600 dark:text-emerald-400 text-xs font-bold hover:bg-emerald-100">+15</button>
                    </div>
                </div>

                <!-- Slider Mode -->
                <div id="sliderModeContainer" class="space-y-4">
                    <div class="flex justify-between text-xs text-slate-400 font-medium">
                        <span>1 แผ่น</span>
                        <span id="maxRangeLabel">100 แผ่น</span>
                    </div>
                    <input type="range" id="quantityRange" min="1" max="100" value="1" oninput="updateQuantity(this.value)" class="w-full accent-emerald-600 bg-slate-100 dark:bg-slate-800 h-2.5 rounded-lg cursor-pointer">
                    <div class="flex justify-center gap-2 pt-2">
                        <button onclick="setMaxRange(100)" id="btnMax100" class="text-xs px-4 py-2 rounded-xl bg-emerald-600 text-white font-semibold shadow-sm">ช่วง 1 - 100</button>
                        <button onclick="setMaxRange(1000)" id="btnMax1000" class="text-xs px-4 py-2 rounded-xl bg-slate-100 dark:bg-slate-800 border border-slate-200 dark:border-slate-700 text-slate-600 dark:text-slate-300 font-medium">ช่วง 1 - 1000</button>
                    </div>
                </div>

                <!-- Input Mode -->
                <div id="inputModeContainer" class="hidden space-y-3">
                    <input type="number" id="quantityInput" min="1" value="1" onclick="this.value=''" oninput="updateQuantity(this.value)" class="w-full bg-slate-50 dark:bg-slate-800 border border-slate-200 dark:border-slate-700 rounded-2xl px-4 py-4 text-center text-2xl font-bold text-slate-900 dark:text-white focus:outline-none focus:border-emerald-500">
                </div>
            </div>

            <!-- Section 3: Extra Charges & Discounts -->
            <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                <div class="bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-800 rounded-3xl p-5 flex flex-col gap-4 shadow-sm">
                    <div class="flex items-center justify-between">
                        <div class="flex items-center gap-3.5">
                            <div class="w-11 h-11 rounded-2xl bg-slate-100 dark:bg-slate-800 text-slate-600 dark:text-slate-300 flex items-center justify-center">
                                <i class="fa-solid fa-screwdriver-wrench"></i>
                            </div>
                            <div>
                                <h4 id="extraServiceTitle" class="font-bold text-sm text-slate-900 dark:text-white">เพิ่มค่าบริการเสริม (+10.00 ฿)</h4>
                                <p class="text-xs text-slate-400">เข้าเล่ม, เคลือบพลาสติก ฯลฯ</p>
                            </div>
                        </div>
                        <label class="relative inline-flex items-center cursor-pointer">
                            <input type="checkbox" id="extraServiceToggle" onchange="calculateTotal(); saveData();" class="sr-only peer">
                            <div class="w-11 h-6 bg-slate-200 dark:bg-slate-800 peer-focus:outline-none rounded-full peer peer-checked:after:translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-[2px] after:left-[2px] after:bg-white after:border-slate-300 after:border after:rounded-full after:h-5 after:w-5 after:transition-all peer-checked:bg-emerald-600"></div>
                        </label>
                    </div>
                    <!-- Direct price config and toggle right below -->
                    <div class="pt-3 border-t border-slate-100 dark:border-slate-800 flex items-center justify-between gap-3">
                        <span class="text-xs font-semibold text-slate-600 dark:text-slate-400">กำหนดราคาค่าบริการ (บาท):</span>
                        <div class="flex items-center gap-2">
                            <input type="number" step="1" id="quickExtraPriceInput" oninput="updateQuickExtraPrice(this.value)" class="w-24 bg-slate-50 dark:bg-slate-800 border border-slate-200 dark:border-slate-700 rounded-xl px-3 py-1.5 text-center text-xs font-bold text-slate-900 dark:text-white focus:outline-none focus:border-emerald-500" value="10">
                            <span class="text-xs text-slate-500 font-semibold">฿</span>
                        </div>
                    </div>
                </div>

                <div class="bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-800 rounded-3xl p-5 flex items-center justify-between shadow-sm">
                    <div class="flex items-center gap-3.5">
                        <div class="w-11 h-11 rounded-2xl bg-slate-100 dark:bg-slate-800 text-slate-600 dark:text-slate-300 flex items-center justify-center">
                            <i class="fa-solid fa-percent"></i>
                        </div>
                        <div>
                            <h4 class="font-bold text-sm text-slate-900 dark:text-white">ลดราคาอัตโนมัติ</h4>
                            <p class="text-xs text-slate-400">ลด 5% เมื่อพิมพ์ 50 แผ่นขึ้นไป</p>
                        </div>
                    </div>
                    <label class="relative inline-flex items-center cursor-pointer">
                        <input type="checkbox" id="autoDiscountToggle" onchange="calculateTotal()" class="sr-only peer">
                        <div class="w-11 h-6 bg-slate-200 dark:bg-slate-800 peer-focus:outline-none rounded-full peer peer-checked:after:translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-[2px] after:left-[2px] after:bg-white after:border-slate-300 after:border after:rounded-full after:h-5 after:w-5 after:transition-all peer-checked:bg-emerald-600"></div>
                    </label>
                </div>
            </div>

        </div>

        <!-- Right Panel (Summary & Checkout) -->
        <div class="space-y-6">
            <div class="bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-800 rounded-3xl p-6 shadow-sm sticky top-6">
                <div class="flex justify-between items-center mb-5 pb-3.5 border-b border-slate-100 dark:border-slate-800">
                    <h3 class="font-bold text-slate-900 dark:text-white flex items-center gap-2 text-base">
                        <i class="fa-solid fa-receipt text-emerald-600 dark:text-emerald-400"></i> สรุปรายการคำนวณ
                    </h3>
                    <span id="currentDate" class="text-xs text-slate-400 font-medium"></span>
                </div>

                <div class="space-y-3.5 mb-5 text-sm">
                    <div class="flex justify-between items-center">
                        <span id="summaryTypeName" class="text-slate-500 dark:text-slate-400 font-medium">กระดาษเปล่า (A4)</span>
                        <span id="summaryUnitPrice" class="font-semibold text-slate-900 dark:text-white">1.00 ฿ / แผ่น</span>
                    </div>
                    <div id="summarySideRow" class="flex justify-between items-center">
                        <span class="text-slate-500 dark:text-slate-400 font-medium">รูปแบบ</span>
                        <span id="summarySideText" class="font-semibold text-slate-900 dark:text-white">1 ด้าน</span>
                    </div>
                    <div class="flex justify-between items-center">
                        <span class="text-slate-500 dark:text-slate-400 font-medium">จำนวนทั้งหมด</span>
                        <span id="summaryQuantity" class="font-semibold text-slate-900 dark:text-white">1 แผ่น</span>
                    </div>
                    <div id="extraRow" class="hidden flex justify-between items-center text-amber-600 dark:text-amber-400 font-medium">
                        <span id="summaryExtraLabel">ค่าบริการเสริม</span>
                        <span id="summaryExtraPrice">+ 10.00 ฿</span>
                    </div>
                    <div id="discountRow" class="hidden flex justify-between items-center text-emerald-600 dark:text-emerald-400 font-medium">
                        <span>ส่วนลดพิเศษ</span>
                        <span>- 5%</span>
                    </div>
                </div>

                <div class="bg-slate-50 dark:bg-slate-950 border border-slate-200 dark:border-slate-800 rounded-2xl p-4.5 mb-6">
                    <div class="flex justify-between items-end">
                        <div>
                            <p class="text-xs text-slate-400 font-medium mb-1">ยอดชำระสุทธิ</p>
                            <h2 class="text-3xl md:text-4xl font-black text-emerald-600 dark:text-emerald-400"><span id="totalAmount">1.00</span> <span class="text-sm font-normal text-slate-400">บาท</span></h2>
                        </div>
                        <span class="bg-emerald-50 dark:bg-emerald-500/10 text-emerald-600 dark:text-emerald-400 text-xs px-2.5 py-1 rounded-lg border border-emerald-100 dark:border-emerald-500/20 font-semibold">พร้อมชำระ</span>
                    </div>
                </div>

                <!-- Separate Cart List Section Below Total (Standard Layout) -->
                <div class="mb-6 pt-4 border-t border-slate-100 dark:border-slate-800">
                    <div class="flex justify-between items-center mb-3">
                        <h4 class="text-xs font-bold text-slate-700 dark:text-slate-300 flex items-center gap-1.5">
                            <i class="fa-solid fa-cart-shopping text-emerald-600"></i> รายการในตะกร้า (<span id="inlineCartCount">0</span>)
                        </h4>
                        <button onclick="clearCart()" class="text-[11px] text-rose-500 hover:underline">ล้างตะกร้า</button>
                    </div>
                    <div id="inlineCartList" class="space-y-2 max-h-48 overflow-y-auto pr-1 text-xs">
                        <div class="text-slate-400 text-center py-3 bg-slate-50 dark:bg-slate-950/40 rounded-xl border border-slate-100 dark:border-slate-800">ยังไม่มีสินค้าในตะกร้า</div>
                    </div>
                    <div id="inlineCartTotalContainer" class="flex justify-between items-center mt-3 pt-3 border-t border-slate-100 dark:border-slate-800 hidden">
                        <span class="text-xs font-bold text-slate-600 dark:text-slate-400">รวมราคาสินค้าในตะกร้า</span>
                        <span id="inlineCartTotal" class="text-sm font-black text-emerald-600 dark:text-emerald-400">0.00 ฿</span>
                    </div>
                </div>

                <div class="space-y-2.5">
                    <button onclick="addToCart()" class="w-full bg-slate-100 dark:bg-slate-800 hover:bg-slate-200 dark:hover:bg-slate-700 border border-slate-200 dark:border-slate-700 text-slate-700 dark:text-slate-200 font-semibold py-3.5 rounded-2xl flex items-center justify-center gap-2 transition-all text-sm">
                        <i class="fa-solid fa-cart-plus text-emerald-600 dark:text-emerald-400"></i> เพิ่มลงตะกร้า
                    </button>
                    <button onclick="checkoutNow()" class="w-full bg-emerald-600 hover:bg-emerald-500 text-white font-semibold py-3.5 rounded-2xl flex items-center justify-center gap-2 shadow-lg shadow-emerald-600/25 transition-all text-sm">
                        <i class="fa-solid fa-cash-register"></i> คิดเงินทันที
                    </button>
                </div>
            </div>

            <!-- Help Notice Box -->
            <div class="bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-800 rounded-3xl p-6 text-xs text-slate-500 dark:text-slate-400 space-y-2.5 shadow-sm">
                <p class="font-bold text-slate-900 dark:text-white flex items-center gap-2 text-sm mb-1">
                    <i class="fa-solid fa-circle-info text-emerald-600 dark:text-emerald-400"></i> ข้อแนะนำการใช้งาน
                </p>
                <p>• สามารถปรับเปลี่ยนราคาและเพิ่มประเภทงานพิมพ์ได้ที่ปุ่ม "ตั้งค่าราคา" ด้านบนขวา</p>
                <p>• กดบันทึกข้อความเพื่อจดโน้ตรายการลูกค้าหรือยอดค้างรับเงินได้ตลอดเวลา</p>
            </div>
        </div>

    </main>

    <!-- Modal: Settings Price -->
    <div id="priceModal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 flex items-center justify-center p-4 overflow-y-auto hidden">
        <div class="bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-800 rounded-3xl max-w-lg w-full max-h-[90vh] flex flex-col shadow-2xl my-auto">
            <div class="flex justify-between items-center p-6 pb-4 border-b border-slate-100 dark:border-slate-800 flex-shrink-0">
                <h3 class="font-bold text-lg text-slate-900 dark:text-white">ตั้งค่าราคาประเภทงานพิมพ์และค่าบริการ</h3>
                <button onclick="closePriceModal()" class="text-slate-400 hover:text-slate-600 dark:hover:text-white"><i class="fa-solid fa-xmark text-lg"></i></button>
            </div>
            
            <div class="p-6 overflow-y-auto space-y-4 flex-grow">
                <div id="priceSettingsList" class="space-y-3.5">
                    <!-- Dynamic price inputs -->
                </div>
                
                <!-- Extra service price setting with ON/OFF switch -->
                <div class="pt-4 border-t border-slate-100 dark:border-slate-800 space-y-3">
                    <div class="flex items-center justify-between">
                        <label class="text-xs font-bold text-slate-700 dark:text-slate-300">เปิด/ปิด ใช้งานค่าบริการเสริม</label>
                        <label class="relative inline-flex items-center cursor-pointer">
                            <input type="checkbox" id="editExtraToggle" class="sr-only peer">
                            <div class="w-11 h-6 bg-slate-200 dark:bg-slate-800 peer-focus:outline-none rounded-full peer peer-checked:after:translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-[2px] after:left-[2px] after:bg-white after:border-slate-300 after:border after:rounded-full after:h-5 after:w-5 after:transition-all peer-checked:bg-emerald-600"></div>
                        </label>
                    </div>
                    <div>
                        <label class="text-xs font-bold text-slate-700 dark:text-slate-300 mb-1 block">ตั้งค่าราคาค่าบริการเสริม (บาท)</label>
                        <input type="number" step="1" id="editExtraPriceInput" class="w-full bg-slate-50 dark:bg-slate-800 border border-slate-200 dark:border-slate-700 rounded-xl px-3.5 py-2.5 text-sm font-bold text-slate-900 dark:text-white focus:outline-none focus:border-emerald-500">
                    </div>
                </div>

                <!-- Auto Discount Settings in Modal -->
                <div class="pt-4 border-t border-slate-100 dark:border-slate-800 space-y-3">
                    <h4 class="text-xs font-bold text-slate-700 dark:text-slate-300">ตั้งค่าส่วนลดอัตโนมัติ</h4>
                    <div class="grid grid-cols-2 gap-3">
                        <div>
                            <label class="text-[10px] text-slate-400 font-semibold">ขั้นต่ำ (แผ่นขึ้นไป)</label>
                            <input type="number" id="editDiscountMinQty" class="w-full bg-slate-50 dark:bg-slate-800 border border-slate-200 dark:border-slate-700 rounded-xl px-3 py-2 text-xs font-bold text-slate-900 dark:text-white focus:outline-none focus:border-emerald-500" value="50">
                        </div>
                        <div>
                            <label class="text-[10px] text-slate-400 font-semibold">ส่วนลด (%)</label>
                            <input type="number" step="0.5" id="editDiscountPercent" class="w-full bg-slate-50 dark:bg-slate-800 border border-slate-200 dark:border-slate-700 rounded-xl px-3 py-2 text-xs font-bold text-slate-900 dark:text-white focus:outline-none focus:border-emerald-500" value="5">
                        </div>
                    </div>
                </div>

                <!-- Backup / Restore Section (For Google Sites) -->
                <div class="pt-4 border-t border-slate-100 dark:border-slate-800 space-y-3">
                    <div class="flex items-center gap-2">
                        <h4 class="text-xs font-bold text-slate-700 dark:text-slate-300">สำรองข้อมูล / กู้คืน</h4>
                        <span class="text-[10px] text-rose-500 bg-rose-50 dark:bg-rose-900/30 px-2 py-0.5 rounded-full font-medium">สำหรับ Google Sites</span>
                    </div>
                    <div class="flex gap-2">
                        <button onclick="exportBackup()" class="flex-1 px-4 py-2.5 rounded-xl bg-indigo-50 dark:bg-indigo-500/10 text-indigo-600 dark:text-indigo-400 border border-indigo-100 dark:border-indigo-500/20 text-xs font-bold hover:bg-indigo-100 transition-colors flex justify-center items-center gap-1.5"><i class="fa-solid fa-download"></i> สำรองไฟล์</button>
                        <label class="flex-1 px-4 py-2.5 rounded-xl bg-amber-50 dark:bg-amber-500/10 text-amber-600 dark:text-amber-400 border border-amber-100 dark:border-amber-500/20 text-xs font-bold hover:bg-amber-100 transition-colors cursor-pointer flex justify-center items-center gap-1.5">
                            <i class="fa-solid fa-upload"></i> โหลดไฟล์
                            <input type="file" accept=".json" onchange="importBackup(event)" class="hidden">
                        </label>
                    </div>
                </div>
            </div>

            <div class="p-6 pt-4 flex justify-end gap-2.5 border-t border-slate-100 dark:border-slate-800 flex-shrink-0">
                <button onclick="closePriceModal()" class="px-4 py-2.5 rounded-xl bg-slate-100 dark:bg-slate-800 text-slate-700 dark:text-slate-300 text-xs font-semibold hover:bg-slate-200">ปิด</button>
                <button onclick="savePrices()" class="px-5 py-2.5 rounded-xl bg-emerald-600 text-white text-xs font-semibold hover:bg-emerald-500 shadow-md shadow-emerald-600/20">บันทึกราคา</button>
            </div>
        </div>
    </div>

    <!-- Modal: Notes -->
    <div id="notesModal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
        <div class="bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-800 rounded-3xl max-w-lg w-full p-6 shadow-2xl">
            <div class="flex justify-between items-center mb-5 pb-3 border-b border-slate-100 dark:border-slate-800">
                <h3 class="font-bold text-lg text-slate-900 dark:text-white">บันทึกข้อความ / โน้ตย่อ</h3>
                <button onclick="closeNotesModal()" class="text-slate-400 hover:text-slate-600 dark:hover:text-white"><i class="fa-solid fa-xmark text-lg"></i></button>
            </div>
            <textarea id="notesTextarea" rows="6" placeholder="พิมพ์บันทึกข้อความหรือยอดค้างชำระตรงนี้..." class="w-full bg-slate-50 dark:bg-slate-800 border border-slate-200 dark:border-slate-700 rounded-2xl p-4 text-sm text-slate-900 dark:text-white focus:outline-none focus:border-emerald-500 resize-none"></textarea>
            <div class="mt-5 flex justify-end gap-2.5 pt-3 border-t border-slate-100 dark:border-slate-800">
                <button onclick="closeNotesModal()" class="px-4 py-2.5 rounded-xl bg-slate-100 dark:bg-slate-800 text-slate-700 dark:text-slate-300 text-xs font-semibold">ปิด</button>
                <button onclick="saveNotes()" class="px-5 py-2.5 rounded-xl bg-amber-600 text-white text-xs font-semibold hover:bg-amber-500 shadow-md shadow-amber-600/20">บันทึกข้อความ</button>
            </div>
        </div>
    </div>

    <!-- Modal: Cart -->
    <div id="cartModal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
        <div class="bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-800 rounded-3xl max-w-xl w-full p-6 shadow-2xl max-h-[90vh] flex flex-col">
            <div class="flex justify-between items-center mb-4 pb-3 border-b border-slate-100 dark:border-slate-800 flex-shrink-0">
                <h3 class="font-bold text-lg text-slate-900 dark:text-white flex items-center gap-2"><i class="fa-solid fa-cart-shopping text-emerald-600 dark:text-emerald-400"></i> ตะกร้าสินค้า</h3>
                <button onclick="closeCartModal()" class="text-slate-400 hover:text-slate-600 dark:hover:text-white"><i class="fa-solid fa-xmark text-lg"></i></button>
            </div>
            
            <!-- Cart items list first -->
            <div id="cartItemsList" class="divide-y divide-slate-100 dark:divide-slate-800 max-h-[35vh] overflow-y-auto mb-4 pr-1 flex-grow">
                <!-- Cart items -->
            </div>

            <!-- Total price and payment calculator below cart items -->
            <div class="space-y-3 pt-4 border-t border-slate-100 dark:border-slate-800 flex-shrink-0">
                <div class="flex justify-between items-center">
                    <span class="text-slate-500 dark:text-slate-400 text-sm font-medium">รวมทั้งสิ้นในตะกร้า</span>
                    <span id="cartTotalPrice" class="text-2xl font-black text-emerald-600 dark:text-emerald-400">0.00 บาท</span>
                </div>

                <!-- Cash received input & change calculation -->
                <div class="bg-slate-50 dark:bg-slate-800/50 p-3.5 rounded-2xl border border-slate-200 dark:border-slate-700 space-y-2">
                    <div class="flex justify-between items-center gap-3">
                        <label class="text-xs font-bold text-slate-700 dark:text-slate-300">รับเงินมา (บาท):</label>
                        <input type="number" step="1" id="cashReceivedInput" oninput="calculateChange()" placeholder="0" class="w-36 bg-white dark:bg-slate-900 border border-slate-300 dark:border-slate-600 rounded-xl px-3 py-1.5 text-right font-bold text-emerald-600 dark:text-emerald-400 text-sm focus:outline-none focus:border-emerald-500">
                    </div>
                    <div class="flex justify-between items-center text-sm font-semibold pt-1 border-t border-slate-200/60 dark:border-slate-700/60">
                        <span class="text-slate-600 dark:text-slate-400">เงินทอน:</span>
                        <span id="changeAmountDisplay" class="text-lg font-black text-amber-600 dark:text-amber-400">0.00 บาท</span>
                    </div>
                </div>
            </div>

            <div class="flex justify-between gap-2.5 pt-4 flex-shrink-0">
                <button onclick="clearCart()" class="px-4 py-3 rounded-xl bg-rose-50 dark:bg-rose-500/10 text-rose-600 dark:text-rose-400 border border-rose-100 dark:border-rose-500/20 text-xs font-semibold hover:bg-rose-100">ล้างตะกร้า</button>
                <div class="flex gap-2">
                    <button onclick="closeCartModal()" class="px-4 py-3 rounded-xl bg-slate-100 dark:bg-slate-800 text-slate-700 dark:text-slate-300 text-xs font-semibold">ปิด</button>
                    <button onclick="checkoutCart()" class="px-5 py-3 rounded-xl bg-emerald-600 text-white text-xs font-semibold hover:bg-emerald-500 shadow-md shadow-emerald-600/20">ยืนยันชำระเงิน</button>
                </div>
            </div>
        </div>
    </div>

    <!-- Modal: Sales History -->
    <div id="historyModal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
        <div class="bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-800 rounded-3xl max-w-xl w-full p-6 shadow-2xl max-h-[90vh] flex flex-col">
            <div class="flex justify-between items-center mb-4 pb-3 border-b border-slate-100 dark:border-slate-800 flex-shrink-0">
                <h3 class="font-bold text-lg text-slate-900 dark:text-white flex items-center gap-2"><i class="fa-solid fa-clock-rotate-left text-emerald-600 dark:text-emerald-400"></i> ประวัติการขาย</h3>
                <button onclick="closeHistoryModal()" class="text-slate-400 hover:text-slate-600 dark:hover:text-white"><i class="fa-solid fa-xmark text-lg"></i></button>
            </div>
            <div id="historyItemsList" class="divide-y divide-slate-100 dark:divide-slate-800 max-h-[45vh] overflow-y-auto mb-4 pr-1 flex-grow">
                <!-- History items -->
            </div>
            <div class="flex justify-between items-center pt-3 border-t border-slate-100 dark:border-slate-800 flex-shrink-0 mb-4">
                <span class="text-xs font-bold text-slate-500">ยอดขายรวมทั้งหมด</span>
                <span id="historyTotalPrice" class="text-xl font-black text-emerald-600 dark:text-emerald-400">0.00 บาท</span>
            </div>
            <div class="flex justify-between gap-2.5 flex-shrink-0 flex-wrap">
                <div class="flex gap-2.5">
                    <button onclick="clearHistory()" class="px-4 py-2.5 rounded-xl bg-rose-50 dark:bg-rose-500/10 text-rose-600 dark:text-rose-400 border border-rose-100 dark:border-rose-500/20 text-xs font-semibold hover:bg-rose-100">ล้างประวัติทั้งหมด</button>
                    <button onclick="exportHistoryCSV()" class="px-4 py-2.5 rounded-xl bg-indigo-50 dark:bg-indigo-500/10 text-indigo-600 dark:text-indigo-400 border border-indigo-100 dark:border-indigo-500/20 text-xs font-semibold hover:bg-indigo-100 flex items-center gap-1.5"><i class="fa-solid fa-file-csv"></i> ส่งออก Excel</button>
                </div>
                <button onclick="closeHistoryModal()" class="px-4 py-2.5 rounded-xl bg-slate-100 dark:bg-slate-800 text-slate-700 dark:text-slate-300 text-xs font-semibold">ปิด</button>
            </div>
        </div>
    </div>

    <!-- Modal: Features Showcase -->
    <div id="featuresModal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
        <div class="bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-800 rounded-3xl max-w-md w-full shadow-2xl flex flex-col overflow-hidden animate-fade-in-up">
            <!-- Header -->
            <div class="bg-gradient-to-r from-emerald-600 to-teal-500 p-6 text-white relative">
                <button onclick="closeFeaturesModal()" class="absolute top-4 right-4 text-white/70 hover:text-white transition-colors bg-black/10 hover:bg-black/20 rounded-full w-8 h-8 flex items-center justify-center">
                    <i class="fa-solid fa-xmark text-lg"></i>
                </button>
                <div class="w-12 h-12 bg-white/20 rounded-2xl flex items-center justify-center text-2xl mb-3 backdrop-blur-sm border border-white/20">
                    <i class="fa-solid fa-wand-magic-sparkles"></i>
                </div>
                <h3 class="font-bold text-xl mb-1">มีอะไรใหม่ในอัปเดตนี้?</h3>
                <p class="text-emerald-50 text-xs font-medium">เวอร์ชัน Pro v4.6 Midnight Green</p>
            </div>
            
            <!-- Features List -->
            <div class="p-6 space-y-4 max-h-[60vh] overflow-y-auto">
                <div class="flex gap-3.5">
                    <div class="w-8 h-8 rounded-full bg-emerald-50 dark:bg-emerald-500/10 text-emerald-600 dark:text-emerald-400 flex items-center justify-center flex-shrink-0 text-sm mt-0.5">
                        <i class="fa-solid fa-cloud-arrow-up"></i>
                    </div>
                    <div>
                        <h4 class="font-bold text-sm text-slate-900 dark:text-white">บันทึกข้อมูลปลอดภัย (Cloud & Local)</h4>
                        <p class="text-xs text-slate-500 dark:text-slate-400 mt-1">รีเฟรชหน้าเว็บหรือปิดเบราว์เซอร์ข้อมูลก็ไม่หาย ระบบจัดการให้อัตโนมัติ</p>
                    </div>
                </div>
                <div class="flex gap-3.5">
                    <div class="w-8 h-8 rounded-full bg-emerald-50 dark:bg-emerald-500/10 text-emerald-600 dark:text-emerald-400 flex items-center justify-center flex-shrink-0 text-sm mt-0.5">
                        <i class="fa-solid fa-moon"></i>
                    </div>
                    <div>
                        <h4 class="font-bold text-sm text-slate-900 dark:text-white">ธีมตั้งต้น Midnight Green</h4>
                        <p class="text-xs text-slate-500 dark:text-slate-400 mt-1">สวยงาม ถนอมสายตา ด้วยโทนสีเขียวเหนี่ยวทรัพย์ที่ดูพรีเมียมยิ่งขึ้น</p>
                    </div>
                </div>
                <div class="flex gap-3.5">
                    <div class="w-8 h-8 rounded-full bg-emerald-50 dark:bg-emerald-500/10 text-emerald-600 dark:text-emerald-400 flex items-center justify-center flex-shrink-0 text-sm mt-0.5">
                        <i class="fa-solid fa-calculator"></i>
                    </div>
                    <div>
                        <h4 class="font-bold text-sm text-slate-900 dark:text-white">ระบบตะกร้าและคำนวณเงินทอน</h4>
                        <p class="text-xs text-slate-500 dark:text-slate-400 mt-1">เลือกสินค้าหลายรายการลงตะกร้า พร้อมช่องกรอกยอดรับเงินเพื่อคำนวณเงินทอนให้อัตโนมัติ</p>
                    </div>
                </div>
                <div class="flex gap-3.5">
                    <div class="w-8 h-8 rounded-full bg-emerald-50 dark:bg-emerald-500/10 text-emerald-600 dark:text-emerald-400 flex items-center justify-center flex-shrink-0 text-sm mt-0.5">
                        <i class="fa-solid fa-font"></i>
                    </div>
                    <div>
                        <h4 class="font-bold text-sm text-slate-900 dark:text-white">ฟอนต์ Noto Sans Thai</h4>
                        <p class="text-xs text-slate-500 dark:text-slate-400 mt-1">อ่านง่าย สบายตา จัดเรียง UI ให้พอดีหน้าจอ ใช้งานลื่นไหลมากยิ่งขึ้น</p>
                    </div>
                </div>
            </div>

            <!-- Footer -->
            <div class="p-4 border-t border-slate-100 dark:border-slate-800 bg-slate-50 dark:bg-slate-900/50 flex justify-end">
                <button onclick="closeFeaturesModal()" class="px-5 py-2.5 rounded-xl bg-emerald-600 text-white text-sm font-semibold hover:bg-emerald-500 shadow-md shadow-emerald-600/20 w-full transition-colors">
                    รับทราบและเริ่มใช้งาน
                </button>
            </div>
        </div>
    </div>

    <!-- Modal: Payment (For Checkout Now) -->
    <div id="paymentModal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
        <div class="bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-800 rounded-3xl max-w-sm w-full p-6 shadow-2xl flex flex-col animate-fade-in-up">
            <div class="flex justify-between items-center mb-4 pb-3 border-b border-slate-100 dark:border-slate-800">
                <h3 class="font-bold text-lg text-slate-900 dark:text-white flex items-center gap-2"><i class="fa-solid fa-cash-register text-emerald-600 dark:text-emerald-400"></i> รับชำระเงิน</h3>
                <button onclick="closePaymentModal()" class="text-slate-400 hover:text-slate-600 dark:hover:text-white"><i class="fa-solid fa-xmark text-lg"></i></button>
            </div>
            
            <div class="space-y-4">
                <div class="flex justify-between items-center">
                    <span class="text-slate-500 dark:text-slate-400 text-sm font-medium">ยอดชำระสุทธิ</span>
                    <span class="text-3xl font-black text-emerald-600 dark:text-emerald-400"><span id="paymentTotalAmount">0.00</span> <span class="text-sm font-normal text-slate-400">บาท</span></span>
                </div>

                <div class="bg-slate-50 dark:bg-slate-800/50 p-4 rounded-2xl border border-slate-200 dark:border-slate-700 space-y-3">
                    <div>
                        <label class="text-xs font-bold text-slate-700 dark:text-slate-300 block mb-1">รับเงินมา (บาท):</label>
                        <input type="number" step="1" id="paymentCashInput" oninput="calculatePaymentChange()" placeholder="0" class="w-full bg-white dark:bg-slate-900 border border-slate-300 dark:border-slate-600 rounded-xl px-4 py-2 text-right font-bold text-emerald-600 dark:text-emerald-400 text-lg focus:outline-none focus:border-emerald-500">
                    </div>
                    <div class="flex justify-between items-center text-sm font-semibold pt-2 border-t border-slate-200/60 dark:border-slate-700/60">
                        <span class="text-slate-600 dark:text-slate-400">เงินทอน:</span>
                        <span id="paymentChangeDisplay" class="text-xl font-black text-amber-600 dark:text-amber-400">0.00 บาท</span>
                    </div>
                </div>
            </div>

            <div class="flex justify-end gap-2.5 pt-5 mt-2 border-t border-slate-100 dark:border-slate-800">
                <button onclick="closePaymentModal()" class="px-4 py-2.5 rounded-xl bg-slate-100 dark:bg-slate-800 text-slate-700 dark:text-slate-300 text-xs font-semibold hover:bg-slate-200">ยกเลิก</button>
                <button onclick="confirmPayment()" class="px-5 py-2.5 rounded-xl bg-emerald-600 text-white text-xs font-semibold hover:bg-emerald-500 shadow-md shadow-emerald-600/20">ตกลง / บันทึกประวัติ</button>
            </div>
        </div>
    </div>

    <!-- Modal: Quick Calculator (Floating & Draggable) -->
    <div id="calcModal" class="fixed top-20 right-4 md:right-10 z-[60] hidden shadow-2xl rounded-3xl" style="touch-action: none;">
        <div class="bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-800 rounded-3xl w-[280px] min-w-[240px] max-w-[80vw] min-h-[380px] max-h-[80vh] p-5 shadow-2xl flex flex-col" style="resize: both; overflow: hidden;">
            <!-- Drag Handle -->
            <div id="calcDragHandle" class="flex justify-between items-center mb-4 pb-3 border-b border-slate-100 dark:border-slate-800 cursor-move select-none active:cursor-grabbing shrink-0">
                <h3 class="font-bold text-base text-slate-900 dark:text-white flex items-center gap-2 pointer-events-none"><i class="fa-solid fa-calculator text-indigo-600 dark:text-indigo-400"></i> คิดเลขด่วน</h3>
                <button onclick="closeCalcModal()" class="text-slate-400 hover:text-slate-600 dark:hover:text-white cursor-pointer hover:bg-slate-100 dark:hover:bg-slate-800 w-8 h-8 rounded-full flex items-center justify-center transition-colors"><i class="fa-solid fa-xmark text-lg"></i></button>
            </div>
            
            <div class="bg-slate-50 dark:bg-slate-800/80 rounded-2xl p-4 mb-4 text-right overflow-hidden shadow-inner border border-slate-100 dark:border-slate-700/50 shrink-0">
                <div id="calcHistoryDisplay" class="text-xs text-slate-400 min-h-[16px] mb-1 truncate"></div>
                <div id="calcDisplay" class="text-3xl font-black text-slate-900 dark:text-white tracking-tight truncate">0</div>
            </div>

            <div class="grid grid-cols-4 grid-rows-5 gap-2 flex-grow">
                <button onclick="calcClear()" class="col-span-2 rounded-xl bg-rose-50 dark:bg-rose-500/10 text-rose-600 dark:text-rose-400 font-bold hover:bg-rose-100 dark:hover:bg-rose-500/20 text-sm transition-colors">C</button>
                <button onclick="calcPress('Backspace')" class="rounded-xl bg-amber-50 dark:bg-amber-500/10 text-amber-600 dark:text-amber-400 font-bold hover:bg-amber-100 dark:hover:bg-amber-500/20 text-sm transition-colors"><i class="fa-solid fa-delete-left"></i></button>
                <button onclick="calcPress('/')" class="rounded-xl bg-slate-100 dark:bg-slate-800 text-slate-700 dark:text-slate-300 font-bold hover:bg-slate-200 dark:hover:bg-slate-700 text-sm transition-colors">÷</button>
                
                <button onclick="calcPress('7')" class="rounded-xl bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-700 text-slate-900 dark:text-white font-bold hover:bg-slate-50 dark:hover:bg-slate-800 text-sm shadow-sm transition-colors">7</button>
                <button onclick="calcPress('8')" class="rounded-xl bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-700 text-slate-900 dark:text-white font-bold hover:bg-slate-50 dark:hover:bg-slate-800 text-sm shadow-sm transition-colors">8</button>
                <button onclick="calcPress('9')" class="rounded-xl bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-700 text-slate-900 dark:text-white font-bold hover:bg-slate-50 dark:hover:bg-slate-800 text-sm shadow-sm transition-colors">9</button>
                <button onclick="calcPress('*')" class="rounded-xl bg-slate-100 dark:bg-slate-800 text-slate-700 dark:text-slate-300 font-bold hover:bg-slate-200 dark:hover:bg-slate-700 text-sm transition-colors">×</button>
                
                <button onclick="calcPress('4')" class="rounded-xl bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-700 text-slate-900 dark:text-white font-bold hover:bg-slate-50 dark:hover:bg-slate-800 text-sm shadow-sm transition-colors">4</button>
                <button onclick="calcPress('5')" class="rounded-xl bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-700 text-slate-900 dark:text-white font-bold hover:bg-slate-50 dark:hover:bg-slate-800 text-sm shadow-sm transition-colors">5</button>
                <button onclick="calcPress('6')" class="rounded-xl bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-700 text-slate-900 dark:text-white font-bold hover:bg-slate-50 dark:hover:bg-slate-800 text-sm shadow-sm transition-colors">6</button>
                <button onclick="calcPress('-')" class="rounded-xl bg-slate-100 dark:bg-slate-800 text-slate-700 dark:text-slate-300 font-bold hover:bg-slate-200 dark:hover:bg-slate-700 text-sm transition-colors">-</button>
                
                <button onclick="calcPress('1')" class="rounded-xl bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-700 text-slate-900 dark:text-white font-bold hover:bg-slate-50 dark:hover:bg-slate-800 text-sm shadow-sm transition-colors">1</button>
                <button onclick="calcPress('2')" class="rounded-xl bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-700 text-slate-900 dark:text-white font-bold hover:bg-slate-50 dark:hover:bg-slate-800 text-sm shadow-sm transition-colors">2</button>
                <button onclick="calcPress('3')" class="rounded-xl bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-700 text-slate-900 dark:text-white font-bold hover:bg-slate-50 dark:hover:bg-slate-800 text-sm shadow-sm transition-colors">3</button>
                <button onclick="calcPress('+')" class="rounded-xl bg-slate-100 dark:bg-slate-800 text-slate-700 dark:text-slate-300 font-bold hover:bg-slate-200 dark:hover:bg-slate-700 text-sm transition-colors">+</button>
                
                <button onclick="calcPress('0')" class="col-span-2 rounded-xl bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-700 text-slate-900 dark:text-white font-bold hover:bg-slate-50 dark:hover:bg-slate-800 text-sm shadow-sm transition-colors">0</button>
                <button onclick="calcPress('.')" class="rounded-xl bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-700 text-slate-900 dark:text-white font-bold hover:bg-slate-50 dark:hover:bg-slate-800 text-sm shadow-sm transition-colors">.</button>
                <button onclick="calcCalculate()" class="rounded-xl bg-indigo-600 text-white font-bold hover:bg-indigo-500 shadow-md shadow-indigo-600/20 text-sm transition-colors">=</button>
            </div>
        </div>
    </div>

    <!-- Toast Notification Element -->
    <div id="toast" class="fixed bottom-6 right-6 z-50 transform translate-y-20 opacity-0 transition-all duration-300 pointer-events-none">
        <div class="bg-slate-900 dark:bg-white text-white dark:text-slate-900 px-4 py-3 rounded-2xl shadow-xl flex items-center gap-3 border border-slate-700 dark:border-slate-200 text-xs font-bold">
            <i id="toastIcon" class="fa-solid fa-circle-check text-emerald-400 text-base"></i>
            <span id="toastMsg">แจ้งเตือนสำเร็จ</span>
        </div>
    </div>

    <!-- Firebase Integration -->
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAuth, signInAnonymously, signInWithCustomToken } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { getFirestore, doc, setDoc, onSnapshot, collection, deleteDoc } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

        // =====================================================================
        // 🚀 ตั้งค่าฐานข้อมูลสำหรับ GOOGLE SITES (หากต้องการให้ข้อมูลซิงค์ตลอดเวลา)
        // ให้นำ Config จาก Firebase Console ของคุณมาวางแทน null ด้านล่างนี้
        // ตัวอย่าง: const USER_FIREBASE_CONFIG = { apiKey: "AIza...", authDomain: "...", projectId: "..." };
        // =====================================================================
        const USER_FIREBASE_CONFIG = null; 
        
        let app, db, auth, userId;
        const appId = typeof __app_id !== 'undefined' ? __app_id : 'print-calc-app';
        const firebaseConfig = typeof __firebase_config !== 'undefined' ? JSON.parse(__firebase_config) : USER_FIREBASE_CONFIG;

        if (firebaseConfig) {
            try {
                app = initializeApp(firebaseConfig);
                db = getFirestore(app);
                auth = getAuth(app);

                const initAuth = async () => {
                    try {
                        if (typeof __initial_auth_token !== 'undefined' && __initial_auth_token) {
                            await signInWithCustomToken(auth, __initial_auth_token);
                        } else {
                            await signInAnonymously(auth);
                        }
                        
                        if (!auth.currentUser) return;
                        userId = auth.currentUser.uid;
                        
                        // 💡 เปลี่ยนมาใช้ Public Path แบบเดียวกับระบบ Admin 
                        // เพื่อแก้ปัญหา Google Sites Iframe รีเซ็ต User ID เมื่อรีเฟรช
                        const docRef = doc(db, 'artifacts', appId, 'public', 'data', 'pos_settings', 'config');
                        onSnapshot(docRef, (docSnap) => {
                            if (docSnap.exists()) {
                                const data = docSnap.data();
                                // Only apply if it's newer or we just loaded
                                if (window.applyCloudData) {
                                    window.applyCloudData(data);
                                }
                            }
                        }, (error) => {
                            console.error("Firebase Snapshot Error:", error);
                        });

                        // Listen to Sales History Collection (Admin Dashboard Style)
                        const historyRef = collection(db, 'artifacts', appId, 'public', 'data', 'pos_history');
                        onSnapshot(historyRef, (snapshot) => {
                            const historyData = [];
                            snapshot.forEach(d => historyData.push(d.data()));
                            // Sort in memory (newest first)
                            historyData.sort((a, b) => b.id - a.id); 
                            if (window.updateCloudHistory) {
                                window.updateCloudHistory(historyData);
                            }
                        }, (error) => {
                            console.error("History Snapshot Error:", error);
                        });

                    } catch (e) {
                        console.error("Firebase Auth Error:", e);
                    }
                };
                initAuth();
            } catch(e) {
                console.error("Firebase Init Error:", e);
            }
        }

        window.saveToCloud = async function(dataPayload) {
            if (!db) return;
            try {
                const docRef = doc(db, 'artifacts', appId, 'public', 'data', 'pos_settings', 'config');
                await setDoc(docRef, dataPayload, { merge: true });
            } catch (e) {
                console.error("Error saving to cloud:", e);
            }
        };

        window.saveSaleToCloud = async function(saleItem) {
            if (!db) return;
            try {
                const historyRef = collection(db, 'artifacts', appId, 'public', 'data', 'pos_history');
                await setDoc(doc(historyRef, saleItem.id.toString()), saleItem);
            } catch (e) {
                console.error("Error saving sale:", e);
            }
        };

        window.deleteSaleFromCloud = async function(saleId) {
            if (!db) return;
            try {
                await deleteDoc(doc(db, 'artifacts', appId, 'public', 'data', 'pos_history', saleId.toString()));
            } catch (e) {
                console.error("Error deleting sale:", e);
            }
        };
    </script>

    <script>
        const STORAGE_KEY_TYPES = 'print_calc_types_v7';
        const STORAGE_KEY_CART = 'print_calc_cart_v7';
        const STORAGE_KEY_HISTORY = 'print_calc_history_v7';
        const STORAGE_KEY_NOTES = 'print_calc_notes_v7';
        const STORAGE_KEY_THEME = 'print_calc_theme_v7';
        const STORAGE_KEY_EXTRA = 'print_calc_extra_v7';
        const STORAGE_KEY_EXTRA_ACTIVE = 'print_calc_extra_active_v7';
        const STORAGE_KEY_DISCOUNT_CONFIG = 'print_calc_disc_config_v7';

        let printTypes = [
            { id: 'a4_plain', name: 'กระดาษเปล่า (A4)', price1Side: 1.00, price2Side: 1.00, isPlain: true, desc: 'ราคา 1.00 ฿' },
            { id: 'black_white', name: 'ขาวดำ', price1Side: 2.00, price2Side: 3.00, isPlain: false, desc: '1 ด้าน: 2.00 ฿ | 2 ด้าน: 3.00 ฿' },
            { id: 'color_slight', name: 'สีสันน้อย', price1Side: 4.00, price2Side: 7.00, isPlain: false, desc: '1 ด้าน: 4.00 ฿ | 2 ด้าน: 7.00 ฿' },
            { id: 'color', name: 'สีสัน', price1Side: 6.00, price2Side: 11.00, isPlain: false, desc: '1 ด้าน: 6.00 ฿ | 2 ด้าน: 11.00 ฿' },
            { id: 'color_heavy', name: 'สีสันมาก', price1Side: 10.00, price2Side: 19.00, isPlain: false, desc: '1 ด้าน: 10.00 ฿ | 2 ด้าน: 19.00 ฿' },
            { id: 'custom', name: 'กำหนดเอง', price1Side: 8.00, price2Side: 15.00, isPlain: false, isCustom: true, desc: 'กำหนดราคาเอง (ลดค่ากระดาษด้าน 2)' }
        ];

        let cart = [];
        let salesHistory = [];
        let extraServicePrice = 10.00;
        let discountMinQty = 50;
        let discountPercent = 5;
        let selectedTypeId = 'a4_plain';
        let currentSide = 1;
        let currentQuantity = 1;
        let maxRange = 100;
        let activeMode = 'slider';
        let currentCartTotal = 0;
        let pendingCheckoutData = null;

        window.onload = function () {
            loadLocalStorageData();
            renderPrintTypes();
            updateSideSelectorUI();
            updateExtraServiceUI();
            updateAutoDiscountUI();
            calculateTotal();
            updateCartCount();
            updateHistoryCount();
            document.getElementById('currentDate').innerText = new Date().toLocaleDateString('th-TH', { year: 'numeric', month: 'short', day: 'numeric' });
        };

        function loadLocalStorageData() {
            try {
                const savedTypes = localStorage.getItem(STORAGE_KEY_TYPES);
                if (savedTypes) printTypes = JSON.parse(savedTypes);

                const savedCart = localStorage.getItem(STORAGE_KEY_CART);
                if (savedCart) cart = JSON.parse(savedCart);

                const savedHistory = localStorage.getItem(STORAGE_KEY_HISTORY);
                if (savedHistory) salesHistory = JSON.parse(savedHistory);

                const savedNotes = localStorage.getItem(STORAGE_KEY_NOTES);
                if (savedNotes) document.getElementById('notesTextarea').value = savedNotes;

                const savedExtra = localStorage.getItem(STORAGE_KEY_EXTRA);
                if (savedExtra !== null) extraServicePrice = parseFloat(savedExtra);

                const savedExtraActive = localStorage.getItem(STORAGE_KEY_EXTRA_ACTIVE);
                if (savedExtraActive !== null) {
                    document.getElementById('extraServiceToggle').checked = savedExtraActive === 'true';
                }

                const savedDiscConfig = localStorage.getItem(STORAGE_KEY_DISCOUNT_CONFIG);
                if (savedDiscConfig) {
                    const discData = JSON.parse(savedDiscConfig);
                    discountMinQty = discData.minQty ?? 50;
                    discountPercent = discData.percent ?? 5;
                }

                const savedTheme = localStorage.getItem(STORAGE_KEY_THEME);
                if (savedTheme === 'light') {
                    document.getElementById('mainBody').classList.remove('dark-mode', 'dark');
                    document.getElementById('themeIcon').className = 'fa-solid fa-moon';
                    document.getElementById('themeLabel').innerText = 'โหมดมืด';
                } else {
                    document.getElementById('mainBody').classList.add('dark-mode', 'dark');
                    document.getElementById('themeIcon').className = 'fa-solid fa-sun';
                    document.getElementById('themeLabel').innerText = 'โหมดสว่าง';
                }
            } catch (e) {
                console.error("Error loading localStorage", e);
            }
        }

        function saveLocalStorageData() {
            try {
                localStorage.setItem(STORAGE_KEY_TYPES, JSON.stringify(printTypes));
                localStorage.setItem(STORAGE_KEY_CART, JSON.stringify(cart));
                localStorage.setItem(STORAGE_KEY_HISTORY, JSON.stringify(salesHistory));
                localStorage.setItem(STORAGE_KEY_EXTRA, extraServicePrice);
                localStorage.setItem(STORAGE_KEY_EXTRA_ACTIVE, document.getElementById('extraServiceToggle').checked);
                localStorage.setItem(STORAGE_KEY_DISCOUNT_CONFIG, JSON.stringify({ minQty: discountMinQty, percent: discountPercent }));
                const isDark = document.getElementById('mainBody').classList.contains('dark');
                localStorage.setItem(STORAGE_KEY_THEME, isDark ? 'dark' : 'light');
            } catch (e) {
                console.error("Error saving localStorage", e);
            }
        }

        let isApplyingCloudData = false;

        window.applyCloudData = function(data) {
            isApplyingCloudData = true;
            try {
                if (data.printTypes) printTypes = data.printTypes;
                if (data.cart) cart = data.cart;
                // salesHistory is now handled by the separate collection listener
                if (data.extraServicePrice !== undefined) extraServicePrice = data.extraServicePrice;
                if (data.extraServiceActive !== undefined) document.getElementById('extraServiceToggle').checked = data.extraServiceActive;
                if (data.discountMinQty !== undefined) discountMinQty = data.discountMinQty;
                if (data.discountPercent !== undefined) discountPercent = data.discountPercent;
                if (data.notes !== undefined && document.getElementById('notesTextarea').value !== data.notes) {
                    document.getElementById('notesTextarea').value = data.notes;
                }
                
                if (data.theme) {
                    const body = document.getElementById('mainBody');
                    if (data.theme === 'light') {
                        body.classList.remove('dark-mode', 'dark');
                        document.getElementById('themeIcon').className = 'fa-solid fa-moon';
                        document.getElementById('themeLabel').innerText = 'โหมดมืด';
                    } else {
                        body.classList.add('dark-mode', 'dark');
                        document.getElementById('themeIcon').className = 'fa-solid fa-sun';
                        document.getElementById('themeLabel').innerText = 'โหมดสว่าง';
                    }
                }

                // Update UI based on new data
                renderPrintTypes();
                updateSideSelectorUI();
                updateExtraServiceUI();
                updateAutoDiscountUI();
                calculateTotal();
                updateCartCount();
                updateHistoryCount();
                saveLocalStorageData(); // Keep local storage in sync with cloud
            } finally {
                isApplyingCloudData = false;
            }
        };

        window.updateCloudHistory = function(data) {
            salesHistory = data;
            saveLocalStorageData();
            updateHistoryCount();
            if (!document.getElementById('historyModal').classList.contains('hidden')) {
                openHistoryModal(); // Refresh modal UI if it's currently open
            }
        };

        function saveData() {
            if (isApplyingCloudData) return; // Prevent loop when receiving cloud updates
            
            saveLocalStorageData();
            
            if (window.saveToCloud) {
                const isDark = document.getElementById('mainBody').classList.contains('dark');
                window.saveToCloud({
                    printTypes: printTypes,
                    cart: cart,
                    // Note: salesHistory is deliberately excluded here as it's saved to its own collection
                    extraServicePrice: extraServicePrice,
                    extraServiceActive: document.getElementById('extraServiceToggle').checked,
                    discountMinQty: discountMinQty,
                    discountPercent: discountPercent,
                    notes: document.getElementById('notesTextarea').value,
                    theme: isDark ? 'dark' : 'light',
                    lastUpdated: Date.now()
                });
            }
        }

        function updateExtraServiceUI() {
            document.getElementById('extraServiceTitle').innerText = `เพิ่มค่าบริการเสริม (+${extraServicePrice.toFixed(2)} ฿)`;
            document.getElementById('summaryExtraLabel').innerText = 'ค่าบริการเสริม';
            document.getElementById('summaryExtraPrice').innerText = `+ ${extraServicePrice.toFixed(2)} ฿`;
            const quickInput = document.getElementById('quickExtraPriceInput');
            if (quickInput && parseFloat(quickInput.value) !== extraServicePrice) {
                quickInput.value = extraServicePrice;
            }
        }

        function updateAutoDiscountUI() {
            const descEls = document.querySelectorAll('.text-xs.text-slate-400');
            descEls.forEach(el => {
                if (el.innerText.includes('ลด') && el.innerText.includes('แผ่นขึ้นไป')) {
                    el.innerText = `ลด ${discountPercent}% เมื่อพิมพ์ ${discountMinQty} แผ่นขึ้นไป`;
                }
            });
        }

        function updateQuickExtraPrice(val) {
            const parsed = parseFloat(val);
            if (!isNaN(parsed) && parsed >= 0) {
                extraServicePrice = parsed;
                updateExtraServiceUI();
                calculateTotal();
                saveData();
            }
        }

        function calculateTotal() {
            const type = printTypes.find(t => t.id === selectedTypeId) || printTypes[0];
            let unitPrice = type.isPlain ? type.price1Side : (currentSide === 1 ? type.price1Side : type.price2Side);
            if (type.isCustom) {
                unitPrice = currentSide === 1 ? type.price1Side : type.price2Side;
            }

            let currentItemTotal = unitPrice * currentQuantity;

            const extraActive = document.getElementById('extraServiceToggle').checked;
            const extraRow = document.getElementById('extraRow');
            if (extraActive) {
                currentItemTotal += extraServicePrice;
                extraRow.classList.remove('hidden');
            } else {
                extraRow.classList.add('hidden');
            }

            const discountChecked = document.getElementById('autoDiscountToggle').checked;
            const discountRow = document.getElementById('discountRow');
            if (discountChecked && currentQuantity >= discountMinQty) {
                let discAmount = currentItemTotal * (discountPercent / 100);
                currentItemTotal = currentItemTotal - discAmount;
                discountRow.classList.remove('hidden');
                discountRow.querySelector('span:nth-child(2)').innerText = `- ${discountPercent}%`;
            } else {
                discountRow.classList.add('hidden');
            }

            document.getElementById('summaryTypeName').innerText = type.name;
            document.getElementById('summaryUnitPrice').innerText = `${unitPrice.toFixed(2)} ฿ / แผ่น`;
            document.getElementById('summaryQuantity').innerText = `${currentQuantity} แผ่น`;
            
            // นำยอดรวมรายการปัจจุบัน มารวมกับ ยอดรวมทั้งหมดในตะกร้า
            const cartTotal = cart.reduce((sum, item) => sum + item.total, 0);
            const grandTotal = currentItemTotal + cartTotal;

            document.getElementById('totalAmount').innerText = grandTotal.toFixed(2);
        }

        function renderPrintTypes() {
            const grid = document.getElementById('printTypesGrid');
            grid.innerHTML = printTypes.map(t => `
                <button onclick="selectPrintType('${t.id}')" class="p-4 rounded-2xl border text-left transition-all relative flex flex-col justify-between ${selectedTypeId === t.id ? 'bg-emerald-50 dark:bg-emerald-950/30 border-emerald-500 shadow-sm' : 'bg-white dark:bg-slate-900 border-slate-200 dark:border-slate-800 hover:border-slate-300'}">
                    <div class="flex justify-between items-start mb-2">
                        <span class="font-bold text-sm text-slate-900 dark:text-white">${t.name}</span>
                        <div class="w-5 h-5 rounded-full border flex items-center justify-center ${selectedTypeId === t.id ? 'border-emerald-600 bg-emerald-600 text-white' : 'border-slate-300 dark:border-slate-600'}">
                            ${selectedTypeId === t.id ? '<i class="fa-solid fa-check text-[10px]"></i>' : ''}
                        </div>
                    </div>
                    <span class="text-xs text-slate-500 dark:text-slate-400 font-medium">${t.desc}</span>
                </button>
            `).join('');
        }

        function selectPrintType(id) {
            selectedTypeId = id;
            const type = printTypes.find(t => t.id === id);
            const sideContainer = document.getElementById('sideSelectorContainer');
            const customContainer = document.getElementById('customPriceContainer');

            if (type.isPlain) {
                sideContainer.classList.add('hidden');
                customContainer.classList.add('hidden');
                currentSide = 1;
            } else {
                sideContainer.classList.remove('hidden');
                if (type.isCustom) {
                    customContainer.classList.remove('hidden');
                    document.getElementById('mainCustomPriceInput').value = type.price1Side;
                } else {
                    customContainer.classList.add('hidden');
                }
            }

            renderPrintTypes();
            updateSideSelectorUI();
            calculateTotal();
            saveData();
        }

        function updateCustomPrice(val) {
            const parsed = parseFloat(val);
            if (!isNaN(parsed)) {
                const type = printTypes.find(t => t.id === 'custom');
                if (type) {
                    type.price1Side = parsed;
                    type.price2Side = parsed + (parsed - 1.00);
                    type.desc = `กำหนดเอง (1 ด้าน: ${parsed} ฿)`;
                    updateSideSelectorUI();
                    calculateTotal();
                    saveData();
                }
            }
        }

        function setSide(side) {
            currentSide = side;
            updateSideSelectorUI();
            calculateTotal();
        }

        function updateSideSelectorUI() {
            const type = printTypes.find(t => t.id === selectedTypeId) || printTypes[0];
            const btn1 = document.getElementById('side1Btn');
            const btn2 = document.getElementById('side2Btn');
            const tag1 = document.getElementById('side1PriceTag');
            const tag2 = document.getElementById('side2PriceTag');
            const sideText = document.getElementById('summarySideText');
            const sideRow = document.getElementById('summarySideRow');

            if (type.isPlain) {
                sideRow.classList.add('hidden');
                return;
            } else {
                sideRow.classList.remove('hidden');
            }

            let p1 = type.price1Side;
            let p2 = type.price2Side;

            tag1.innerText = `${p1.toFixed(2)} ฿ / แผ่น`;
            tag2.innerText = `${p2.toFixed(2)} ฿ / แผ่น`;
            sideText.innerText = currentSide === 1 ? '1 ด้าน' : '2 ด้าน';

            if (currentSide === 1) {
                btn1.className = "p-3.5 rounded-2xl border text-center transition-all font-bold text-xs bg-emerald-50 dark:bg-emerald-950/30 border-emerald-500 text-emerald-900 dark:text-white shadow-sm";
                btn2.className = "p-3.5 rounded-2xl border text-center transition-all font-bold text-xs bg-slate-50 dark:bg-slate-800/40 border-slate-200 dark:border-slate-700 text-slate-600 dark:text-slate-300";
            } else {
                btn2.className = "p-3.5 rounded-2xl border text-center transition-all font-bold text-xs bg-emerald-50 dark:bg-emerald-950/30 border-emerald-500 text-emerald-900 dark:text-white shadow-sm";
                btn1.className = "p-3.5 rounded-2xl border text-center transition-all font-bold text-xs bg-slate-50 dark:bg-slate-800/40 border-slate-200 dark:border-slate-700 text-slate-600 dark:text-slate-300";
            }
        }

        function setMode(mode) {
            activeMode = mode;
            const sliderBtn = document.getElementById('modeSliderBtn');
            const inputBtn = document.getElementById('modeInputBtn');
            const sliderContainer = document.getElementById('sliderModeContainer');
            const inputContainer = document.getElementById('inputModeContainer');

            if (mode === 'slider') {
                sliderBtn.className = "px-3.5 py-1.5 rounded-xl bg-white dark:bg-emerald-600 text-slate-900 dark:text-white shadow-sm font-semibold transition-all";
                inputBtn.className = "px-3.5 py-1.5 rounded-xl text-slate-500 dark:text-slate-400 font-semibold transition-all";
                sliderContainer.classList.remove('hidden');
                inputContainer.classList.add('hidden');
            } else {
                inputBtn.className = "px-3.5 py-1.5 rounded-xl bg-white dark:bg-emerald-600 text-slate-900 dark:text-white shadow-sm font-semibold transition-all";
                sliderBtn.className = "px-3.5 py-1.5 rounded-xl text-slate-500 dark:text-slate-400 font-semibold transition-all";
                inputContainer.classList.remove('hidden');
                sliderContainer.classList.add('hidden');
            }
        }

        function updateQuantity(val) {
            let q = parseInt(val);
            if (isNaN(q) || q < 1) q = 1;
            if (q > maxRange && activeMode === 'slider') {
                q = maxRange;
                document.getElementById('quantityRange').value = q;
            }
            currentQuantity = q;
            document.getElementById('quantityDisplay').innerText = q;
            document.getElementById('quantityRange').value = q;
            document.getElementById('quantityInput').value = q;
            calculateTotal();
        }

        function adjustQuantity(amount) {
            let newQ = currentQuantity + amount;
            if (newQ < 1) newQ = 1;
            updateQuantity(newQ);
        }

        function setMaxRange(max) {
            maxRange = max;
            const btn100 = document.getElementById('btnMax100');
            const btn1000 = document.getElementById('btnMax1000');
            const range = document.getElementById('quantityRange');
            range.max = max;
            document.getElementById('maxRangeLabel').innerText = `${max} แผ่น`;

            if (max === 100) {
                btn100.className = "text-xs px-4 py-2 rounded-xl bg-emerald-600 text-white font-semibold shadow-sm";
                btn1000.className = "text-xs px-4 py-2 rounded-xl bg-slate-100 dark:bg-slate-800 border border-slate-200 dark:border-slate-700 text-slate-600 dark:text-slate-300 font-medium";
            } else {
                btn1000.className = "text-xs px-4 py-2 rounded-xl bg-emerald-600 text-white font-semibold shadow-sm";
                btn100.className = "text-xs px-4 py-2 rounded-xl bg-slate-100 dark:bg-slate-800 border border-slate-200 dark:border-slate-700 text-slate-600 dark:text-slate-300 font-medium";
            }
        }

        function addToCart() {
            const type = printTypes.find(t => t.id === selectedTypeId) || printTypes[0];
            let unitPrice = type.isPlain ? type.price1Side : (currentSide === 1 ? type.price1Side : type.price2Side);
            if (type.isCustom) unitPrice = currentSide === 1 ? type.price1Side : type.price2Side;

            let subtotal = unitPrice * currentQuantity;
            const extraActive = document.getElementById('extraServiceToggle').checked;
            let itemExtra = extraActive ? extraServicePrice : 0;
            let itemTotal = subtotal + itemExtra;

            const discountChecked = document.getElementById('autoDiscountToggle').checked;
            if (discountChecked && currentQuantity >= discountMinQty) {
                itemTotal = itemTotal * (1 - discountPercent / 100);
            }

            cart.push({
                id: Date.now(),
                name: type.name,
                side: type.isPlain ? '-' : (currentSide === 1 ? '1 ด้าน' : '2 ด้าน'),
                quantity: currentQuantity,
                unitPrice: unitPrice,
                extra: itemExtra,
                total: itemTotal
            });

            updateQuantity(1);
            saveData();
            updateCartCount();
            renderInlineCart();
            showToast('เพิ่มลงตะกร้าเรียบร้อยแล้ว');
        }

        function renderInlineCart() {
            const list = document.getElementById('inlineCartList');
            const countEl = document.getElementById('inlineCartCount');
            const totalContainer = document.getElementById('inlineCartTotalContainer');
            const totalEl = document.getElementById('inlineCartTotal');
            
            countEl.innerText = cart.length;

            if (cart.length === 0) {
                list.innerHTML = `<div class="text-slate-400 text-center py-3 bg-slate-50 dark:bg-slate-950/40 rounded-xl border border-slate-100 dark:border-slate-800">ยังไม่มีสินค้าในตะกร้า</div>`;
                if(totalContainer) totalContainer.classList.add('hidden');
                return;
            }

            list.innerHTML = cart.map((item, idx) => `
                <div class="flex justify-between items-center bg-slate-50 dark:bg-slate-800/50 p-2.5 rounded-xl border border-slate-100 dark:border-slate-800">
                    <div>
                        <span class="font-bold text-slate-900 dark:text-white">${item.name} (${item.side})</span>
                        <div class="text-[10px] text-slate-400">${item.quantity} แผ่น | รวม ${item.total.toFixed(2)} ฿</div>
                    </div>
                    <button onclick="removeFromCart(${idx})" class="text-rose-500 hover:text-rose-700 p-1.5 rounded-lg bg-rose-50 dark:bg-rose-500/10"><i class="fa-solid fa-trash text-xs"></i></button>
                </div>
            `).join('');
            
            const cartTotal = cart.reduce((sum, item) => sum + item.total, 0);
            if(totalContainer) {
                totalContainer.classList.remove('hidden');
                totalEl.innerText = `${cartTotal.toFixed(2)} ฿`;
            }
        }

        function removeFromCart(index) {
            cart.splice(index, 1);
            saveData();
            updateCartCount();
            renderInlineCart();
            showToast('ลบรายการออกจากตะกร้าแล้ว');
        }

        function clearCart() {
            cart = [];
            saveData();
            updateCartCount();
            renderInlineCart();
            showToast('ล้างตะกร้าเรียบร้อยแล้ว');
        }

        function updateCartCount() {
            document.getElementById('cartCount').innerText = cart.length;
            renderInlineCart();
            calculateTotal(); // อัปเดตยอดรวมใหญ่ทุกครั้งที่ตะกร้าเปลี่ยน
        }

        function checkoutNow() {
            const type = printTypes.find(t => t.id === selectedTypeId) || printTypes[0];
            let unitPrice = type.isPlain ? type.price1Side : (currentSide === 1 ? type.price1Side : type.price2Side);
            if (type.isCustom) unitPrice = currentSide === 1 ? type.price1Side : type.price2Side;

            let subtotal = unitPrice * currentQuantity;
            const extraActive = document.getElementById('extraServiceToggle').checked;
            let itemExtra = extraActive ? extraServicePrice : 0;
            let itemTotal = subtotal + itemExtra;

            const discountChecked = document.getElementById('autoDiscountToggle').checked;
            if (discountChecked && currentQuantity >= discountMinQty) {
                itemTotal = itemTotal * (1 - discountPercent / 100);
            }

            const currentItem = {
                name: type.name,
                side: type.isPlain ? '-' : (currentSide === 1 ? '1 ด้าน' : '2 ด้าน'),
                quantity: currentQuantity,
                total: itemTotal
            };

            // รวมสินค้าในตะกร้าทั้งหมด + สินค้าที่กำลังเลือกอยู่
            const allItems = [...cart, currentItem];
            const grandTotal = allItems.reduce((sum, item) => sum + item.total, 0);

            pendingCheckoutData = {
                items: allItems,
                total: grandTotal
            };

            // เปิดหน้าต่างรับชำระเงิน (Payment Modal)
            document.getElementById('paymentTotalAmount').innerText = grandTotal.toFixed(2);
            document.getElementById('paymentCashInput').value = '';
            document.getElementById('paymentChangeDisplay').innerText = '0.00 บาท';
            document.getElementById('paymentChangeDisplay').className = 'text-xl font-black text-amber-600 dark:text-amber-400';
            document.getElementById('paymentModal').classList.remove('hidden');
            
            // Auto focus ช่องใส่เงิน
            setTimeout(() => document.getElementById('paymentCashInput').focus(), 100);
        }

        function closePaymentModal() {
            document.getElementById('paymentModal').classList.add('hidden');
            pendingCheckoutData = null;
        }

        function calculatePaymentChange() {
            if (!pendingCheckoutData) return;
            const received = parseFloat(document.getElementById('paymentCashInput').value) || 0;
            const change = received - pendingCheckoutData.total;
            const changeDisplay = document.getElementById('paymentChangeDisplay');
            if (change >= 0) {
                changeDisplay.innerText = `${change.toFixed(2)} บาท`;
                changeDisplay.className = 'text-xl font-black text-emerald-600 dark:text-emerald-400';
            } else {
                changeDisplay.innerText = `ยังขาดอีก ${Math.abs(change).toFixed(2)} บาท`;
                changeDisplay.className = 'text-xl font-black text-rose-600 dark:text-rose-400';
            }
        }

        function confirmPayment() {
            if (!pendingCheckoutData) return;

            const saleItem = {
                id: Date.now(),
                date: new Date().toLocaleString('th-TH'),
                items: pendingCheckoutData.items,
                total: pendingCheckoutData.total
            };

            salesHistory.unshift(saleItem);
            if (window.saveSaleToCloud) window.saveSaleToCloud(saleItem);

            cart = []; // ล้างตะกร้า
            updateQuantity(1); // รีเซ็ตจำนวนแผ่น
            saveData();
            updateCartCount(); // อัปเดต UI ตะกร้า
            updateHistoryCount();
            calculateTotal(); // อัปเดตยอดรวมใหญ่
            closePaymentModal();
            showToast('คิดเงินรวมและบันทึกประวัติสำเร็จ!');
        }

        function openCartModal() {
            const list = document.getElementById('cartItemsList');
            currentCartTotal = 0;
            if (cart.length === 0) {
                list.innerHTML = `<div class="text-slate-400 text-center py-6">ยังไม่มีสินค้าในตะกร้า</div>`;
            } else {
                list.innerHTML = cart.map((item, idx) => {
                    currentCartTotal += item.total;
                    return `
                        <div class="py-3 flex justify-between items-center">
                            <div>
                                <h4 class="font-bold text-sm text-slate-900 dark:text-white">${item.name} (${item.side})</h4>
                                <p class="text-xs text-slate-400">${item.quantity} แผ่น × ${item.unitPrice.toFixed(2)} ฿ ${item.extra > 0 ? `+ ค่าบริการ ${item.extra} ฿` : ''}</p>
                            </div>
                            <div class="flex items-center gap-3">
                                <span class="font-bold text-sm text-emerald-600">${item.total.toFixed(2)} ฿</span>
                                <button onclick="removeFromCart(${idx}); openCartModal();" class="text-rose-500 hover:text-rose-700"><i class="fa-solid fa-trash"></i></button>
                            </div>
                        </div>
                    `;
                }).join('');
            }
            document.getElementById('cartTotalPrice').innerText = `${currentCartTotal.toFixed(2)} บาท`;
            document.getElementById('cashReceivedInput').value = '';
            document.getElementById('changeAmountDisplay').innerText = '0.00 บาท';
            document.getElementById('cartModal').classList.remove('hidden');
        }

        function calculateChange() {
            const received = parseFloat(document.getElementById('cashReceivedInput').value) || 0;
            const change = received - currentCartTotal;
            const changeDisplay = document.getElementById('changeAmountDisplay');
            if (change >= 0) {
                changeDisplay.innerText = `${change.toFixed(2)} บาท`;
                changeDisplay.className = 'text-lg font-black text-emerald-600 dark:text-emerald-400';
            } else {
                changeDisplay.innerText = `ยังขาดอีก ${Math.abs(change).toFixed(2)} บาท`;
                changeDisplay.className = 'text-lg font-black text-rose-600 dark:text-rose-400';
            }
        }

        function closeCartModal() {
            document.getElementById('cartModal').classList.add('hidden');
        }

        function checkoutCart() {
            if (cart.length === 0) {
                showToast('ไม่มีสินค้าในตะกร้า', 'error');
                return;
            }
            let total = cart.reduce((sum, item) => sum + item.total, 0);
            const saleItem = {
                id: Date.now(),
                date: new Date().toLocaleString('th-TH'),
                items: [...cart],
                total: total
            };
            
            salesHistory.unshift(saleItem);
            if (window.saveSaleToCloud) window.saveSaleToCloud(saleItem);
            
            clearCart();
            updateHistoryCount();
            closeCartModal();
            saveData();
            showToast('ชำระเงินตะกร้าสินค้าสำเร็จ!');
        }

        function openHistoryModal() {
            const list = document.getElementById('historyItemsList');
            let totalSales = 0;
            if (salesHistory.length === 0) {
                list.innerHTML = `<div class="text-slate-400 text-center py-6">ยังไม่มีประวัติการขาย</div>`;
            } else {
                list.innerHTML = salesHistory.map((s, idx) => {
                    totalSales += s.total;
                    return `
                        <div class="py-3.5 space-y-1">
                            <div class="flex justify-between items-center text-xs text-slate-400">
                                <span><i class="fa-regular fa-clock"></i> ${s.date}</span>
                                <div class="flex items-center gap-2">
                                    <span class="font-bold text-emerald-600 dark:text-emerald-400 text-sm">${s.total.toFixed(2)} ฿</span>
                                    <button onclick="removeHistoryItem(${s.id});" class="text-rose-500 hover:text-rose-700 p-1"><i class="fa-solid fa-trash text-xs"></i></button>
                                </div>
                            </div>
                            ${s.items.map(i => `<div class="text-xs text-slate-700 dark:text-slate-300 font-medium">• ${i.name} (${i.side}) จำนวน ${i.quantity} แผ่น</div>`).join('')}
                        </div>
                    `;
                }).join('');
            }
            document.getElementById('historyTotalPrice').innerText = `${totalSales.toFixed(2)} บาท`;
            document.getElementById('historyModal').classList.remove('hidden');
        }

        function closeHistoryModal() {
            document.getElementById('historyModal').classList.add('hidden');
        }

        function updateHistoryCount() {
            document.getElementById('historyCount').innerText = salesHistory.length;
        }

        function removeHistoryItem(id) {
            salesHistory = salesHistory.filter(s => s.id !== id);
            if (window.deleteSaleFromCloud) window.deleteSaleFromCloud(id);
            saveData();
            updateHistoryCount();
            openHistoryModal(); // Refresh list
            showToast('ลบรายการประวัติสำเร็จ');
        }

        function clearHistory() {
            if (window.deleteSaleFromCloud) {
                salesHistory.forEach(s => window.deleteSaleFromCloud(s.id));
            }
            salesHistory = [];
            saveData();
            updateHistoryCount();
            openHistoryModal();
            showToast('ล้างประวัติการขายทั้งหมดแล้ว');
        }

        function exportHistoryCSV() {
            if (salesHistory.length === 0) {
                showToast('ไม่มีข้อมูลประวัติการขายสำหรับส่งออก', 'error');
                return;
            }

            // เพิ่ม BOM (\uFEFF) เพื่อให้ Excel อ่านภาษาไทยได้ถูกต้อง
            let csvContent = "\uFEFF"; 
            csvContent += "วันที่/เวลา,รายละเอียดรายการ,จำนวนแผ่นรวม,ยอดรวม (บาท)\n";

            salesHistory.forEach(sale => {
                const date = sale.date.replace(/,/g, '');
                const items = sale.items.map(i => `${i.name} (${i.side}) x ${i.quantity}`).join(" + ");
                const totalQty = sale.items.reduce((sum, item) => sum + item.quantity, 0);
                const total = sale.total.toFixed(2);
                
                // ใส่เครื่องหมายคำพูดคลุมข้อความที่มีลูกน้ำ เพื่อไม่ให้ CSV คอลัมน์เพี้ยน
                const safeItems = `"${items.replace(/"/g, '""')}"`;
                
                csvContent += `${date},${safeItems},${totalQty},${total}\n`;
            });

            const blob = new Blob([csvContent], { type: 'text/csv;charset=utf-8;' });
            const link = document.createElement("a");
            const url = URL.createObjectURL(blob);
            link.setAttribute("href", url);
            
            const dateStr = new Date().toLocaleDateString('th-TH').replace(/\//g, '-');
            link.setAttribute("download", `ประวัติการขาย_PrintCalc_${dateStr}.csv`);
            link.style.visibility = 'hidden';
            
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
            
            showToast('ดาวน์โหลดไฟล์ CSV สำเร็จ!');
        }

        function openNotesModal() {
            document.getElementById('notesModal').classList.remove('hidden');
        }

        function closeNotesModal() {
            document.getElementById('notesModal').classList.add('hidden');
        }

        function saveNotes() {
            localStorage.setItem(STORAGE_KEY_NOTES, document.getElementById('notesTextarea').value);
            saveData();
            closeNotesModal();
            showToast('บันทึกข้อความเรียบร้อย');
        }

        function toggleTheme() {
            const body = document.getElementById('mainBody');
            const icon = document.getElementById('themeIcon');
            const label = document.getElementById('themeLabel');
            body.classList.toggle('dark-mode');
            body.classList.toggle('dark');

            if (body.classList.contains('dark')) {
                icon.className = 'fa-solid fa-sun';
                label.innerText = 'โหมดสว่าง';
            } else {
                icon.className = 'fa-solid fa-moon';
                label.innerText = 'โหมดมืด';
            }
            saveData();
        }

        function openPriceModal() {
            const list = document.getElementById('priceSettingsList');
            list.innerHTML = printTypes.map((t, index) => `
                <div class="bg-slate-50 dark:bg-slate-800/60 p-4 rounded-2xl border border-slate-200 dark:border-slate-700/70 space-y-2.5">
                    <input type="text" id="editName_${index}" value="${t.name}" class="w-full bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-700 rounded-xl px-3.5 py-2 text-xs font-semibold text-slate-900 dark:text-white">
                    <div class="grid grid-cols-2 gap-2.5">
                        <div>
                            <label class="text-[10px] text-slate-400 font-semibold">${t.isPlain ? 'ราคา (฿)' : (t.isCustom ? 'ราคา 1 ด้าน (฿) [กำหนดเอง]' : 'ราคา 1 ด้าน (฿)')}</label>
                            <input type="number" step="0.5" id="editPrice1_${index}" value="${t.price1Side}" class="w-full bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-700 rounded-xl px-3 py-1.5 text-xs text-slate-900 dark:text-white">
                        </div>
                        ${!t.isPlain ? `
                        <div>
                            <label class="text-[10px] text-slate-400 font-semibold">${t.isCustom ? 'ราคา 2 ด้าน (฿) [คำนวณอัติโนมัติ]' : 'ราคา 2 ด้าน (฿)'}</label>
                            <input type="number" step="0.5" id="editPrice2_${index}" value="${t.price2Side || t.price1Side}" ${t.isCustom ? 'disabled' : ''} class="w-full bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-700 rounded-xl px-3 py-1.5 text-xs text-slate-900 dark:text-white ${t.isCustom ? 'opacity-50 cursor-not-allowed' : ''}">
                        </div>
                        ` : ''}
                    </div>
                </div>
            `).join('');
            document.getElementById('editExtraPriceInput').value = extraServicePrice;
            document.getElementById('editExtraToggle').checked = document.getElementById('extraServiceToggle').checked;
            document.getElementById('editDiscountMinQty').value = discountMinQty;
            document.getElementById('editDiscountPercent').value = discountPercent;
            document.getElementById('priceModal').classList.remove('hidden');
        }

        function savePrices() {
            printTypes.forEach((t, index) => {
                const nameInput = document.getElementById(`editName_${index}`);
                const p1Input = document.getElementById(`editPrice1_${index}`);
                const p2Input = document.getElementById(`editPrice2_${index}`);
                if (nameInput) t.name = nameInput.value;
                if (p1Input) t.price1Side = parseFloat(p1Input.value) || 1;
                if (!t.isPlain) {
                    if (t.isCustom) {
                        t.price2Side = t.price1Side + (t.price1Side - 1.00);
                        t.desc = `กำหนดเอง (1 ด้าน: ${t.price1Side} ฿)`;
                    } else if (p2Input) {
                        t.price2Side = parseFloat(p2Input.value) || t.price1Side;
                        t.desc = `1 ด้าน: ${t.price1Side} ฿ | 2 ด้าน: ${t.price2Side} ฿`;
                    }
                } else {
                    t.price2Side = t.price1Side;
                    t.desc = `ราคา ${t.price1Side} ฿`;
                }
            });

            const extraInputVal = parseFloat(document.getElementById('editExtraPriceInput').value);
            if (!isNaN(extraInputVal)) {
                extraServicePrice = extraInputVal;
            }

            const discMinVal = parseInt(document.getElementById('editDiscountMinQty').value);
            const discPerVal = parseFloat(document.getElementById('editDiscountPercent').value);
            if (!isNaN(discMinVal)) discountMinQty = discMinVal;
            if (!isNaN(discPerVal)) discountPercent = discPerVal;

            document.getElementById('extraServiceToggle').checked = document.getElementById('editExtraToggle').checked;

            saveData();
            renderPrintTypes();
            updateSideSelectorUI();
            updateExtraServiceUI();
            updateAutoDiscountUI();
            calculateTotal();
            closePriceModal();
            showToast('บันทึกการตั้งค่าราคาและส่วนลดเรียบร้อย');
        }

        function closePriceModal() {
            document.getElementById('priceModal').classList.add('hidden');
        }

        function openFeaturesModal() {
            document.getElementById('featuresModal').classList.remove('hidden');
        }

        function closeFeaturesModal() {
            document.getElementById('featuresModal').classList.add('hidden');
        }

        // --- Backup and Restore Logic (For Google Sites workaround) ---
        function exportBackup() {
            const dataToExport = {
                printTypes: printTypes,
                cart: cart,
                salesHistory: salesHistory,
                extraServicePrice: extraServicePrice,
                discountMinQty: discountMinQty,
                discountPercent: discountPercent,
                notes: document.getElementById('notesTextarea').value
            };
            const dataStr = JSON.stringify(dataToExport);
            const blob = new Blob([dataStr], { type: 'application/json' });
            const url = URL.createObjectURL(blob);
            
            const a = document.createElement('a');
            a.href = url;
            a.download = `PrintCalc_Backup_${new Date().toLocaleDateString('th-TH').replace(/\//g, '-')}.json`;
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            URL.revokeObjectURL(url);
            
            showToast('ดาวน์โหลดไฟล์สำรองข้อมูลสำเร็จ!');
        }

        function importBackup(event) {
            const file = event.target.files[0];
            if (!file) return;
            
            const reader = new FileReader();
            reader.onload = function(e) {
                try {
                    const importedData = JSON.parse(e.target.result);
                    
                    if (importedData.printTypes) printTypes = importedData.printTypes;
                    if (importedData.cart) cart = importedData.cart;
                    if (importedData.salesHistory) salesHistory = importedData.salesHistory;
                    if (importedData.extraServicePrice !== undefined) extraServicePrice = importedData.extraServicePrice;
                    if (importedData.discountMinQty !== undefined) discountMinQty = importedData.discountMinQty;
                    if (importedData.discountPercent !== undefined) discountPercent = importedData.discountPercent;
                    if (importedData.notes !== undefined) document.getElementById('notesTextarea').value = importedData.notes;
                    
                    saveData();
                    renderPrintTypes();
                    updateSideSelectorUI();
                    updateExtraServiceUI();
                    updateAutoDiscountUI();
                    calculateTotal();
                    updateCartCount();
                    updateHistoryCount();
                    closePriceModal();
                    
                    showToast('โหลดข้อมูลกู้คืนสำเร็จแล้ว!');
                } catch (error) {
                    console.error("Import Error", error);
                    showToast('ไฟล์ไม่ถูกต้อง หรือเสียหาย', 'error');
                }
                event.target.value = ''; // Reset file input
            };
            reader.readAsText(file);
        }

        // --- Quick Calculator Logic ---
        let calcCurrentExpression = '0';
        let calcEvaluated = false;

        function openCalcModal() {
            document.getElementById('calcModal').classList.remove('hidden');
            if (calcCurrentExpression === '0') {
                calcClear();
            }
        }

        function closeCalcModal() {
            document.getElementById('calcModal').classList.add('hidden');
        }

        function updateCalcDisplay() {
            const display = document.getElementById('calcDisplay');
            display.innerText = calcCurrentExpression;
            // Auto scroll to end if too long
            display.scrollLeft = display.scrollWidth;
        }

        function calcClear() {
            calcCurrentExpression = '0';
            document.getElementById('calcHistoryDisplay').innerText = '';
            updateCalcDisplay();
        }

        function calcPress(val) {
            // Handle number input right after evaluation
            if (calcEvaluated && /[\d\.]/.test(val)) {
                calcCurrentExpression = val;
                calcEvaluated = false;
                document.getElementById('calcHistoryDisplay').innerText = '';
                updateCalcDisplay();
                return;
            }
            calcEvaluated = false;

            if (val === 'Backspace') {
                if (calcCurrentExpression.length > 1) {
                    calcCurrentExpression = calcCurrentExpression.slice(0, -1);
                } else {
                    calcCurrentExpression = '0';
                }
            } else {
                if (calcCurrentExpression === '0' && /[\d]/.test(val)) {
                    calcCurrentExpression = val;
                } else {
                    // Append value
                    calcCurrentExpression += val;
                }
            }
            updateCalcDisplay();
        }

        function calcCalculate() {
            try {
                // Sanitize input to only allow math operations
                let sanitized = calcCurrentExpression.replace(/[^0-9+\-*/.]/g, '');
                if (!sanitized) return;
                
                // Evaluate expression securely using Function instead of direct eval
                const result = new Function('return ' + sanitized)();
                
                // Format floating point safely to avoid 0.30000000000000004
                let finalResult = Number.isInteger(result) ? result : parseFloat(result.toFixed(6));
                
                document.getElementById('calcHistoryDisplay').innerText = calcCurrentExpression + ' =';
                calcCurrentExpression = String(finalResult);
                calcEvaluated = true;
                updateCalcDisplay();
            } catch (e) {
                document.getElementById('calcDisplay').innerText = 'Error';
                setTimeout(calcClear, 1200);
            }
        }

        // --- Draggable Calculator Logic ---
        const draggableCalc = document.getElementById('calcModal');
        const dragHandle = document.getElementById('calcDragHandle');
        let isDraggingCalc = false;
        let dragCurrentX;
        let dragCurrentY;
        let dragInitialX;
        let dragInitialY;
        let dragXOffset = 0;
        let dragYOffset = 0;

        dragHandle.addEventListener('mousedown', dragStart);
        dragHandle.addEventListener('touchstart', dragStart, { passive: false });
        window.addEventListener('mouseup', dragEnd);
        window.addEventListener('touchend', dragEnd);
        window.addEventListener('mousemove', drag);
        window.addEventListener('touchmove', drag, { passive: false });

        function dragStart(e) {
            // Do not drag if clicking the close button
            if (e.target.closest('button')) return;

            if (e.type === "touchstart") {
                dragInitialX = e.touches[0].clientX - dragXOffset;
                dragInitialY = e.touches[0].clientY - dragYOffset;
            } else {
                dragInitialX = e.clientX - dragXOffset;
                dragInitialY = e.clientY - dragYOffset;
            }
            isDraggingCalc = true;
        }

        function dragEnd(e) {
            isDraggingCalc = false;
        }

        function drag(e) {
            if (isDraggingCalc) {
                e.preventDefault(); // Prevent scrolling while dragging

                if (e.type === "touchmove") {
                    dragCurrentX = e.touches[0].clientX - dragInitialX;
                    dragCurrentY = e.touches[0].clientY - dragInitialY;
                } else {
                    dragCurrentX = e.clientX - dragInitialX;
                    dragCurrentY = e.clientY - dragInitialY;
                }

                dragXOffset = dragCurrentX;
                dragYOffset = dragCurrentY;

                draggableCalc.style.transform = `translate3d(${dragCurrentX}px, ${dragCurrentY}px, 0)`;
            }
        }

        function showToast(msg, type = 'success') {
            const toast = document.getElementById('toast');
            const toastMsg = document.getElementById('toastMsg');
            const toastIcon = document.getElementById('toastIcon');

            toastMsg.innerText = msg;
            if (type === 'success') {
                toastIcon.className = 'fa-solid fa-circle-check text-emerald-400 text-base';
            } else {
                toastIcon.className = 'fa-solid fa-circle-exclamation text-rose-400 text-base';
            }

            toast.classList.remove('translate-y-20', 'opacity-0');
            setTimeout(() => {
                toast.classList.add('translate-y-20', 'opacity-0');
            }, 3000);
        }
    </script>
</body>
</html>
