html
<!DOCTYPE html>
<html lang="ku" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Imposter Badini - Infinity Edition</title>
    <style>
        /* دیزاینا تایبەت بۆ ئایفۆن و شاشێن مۆبایلێ */
        * { -webkit-tap-highlight-color: transparent; box-sizing: border-box; }
        
        body {
            font-family: -apple-system, system-ui, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
            background: #000000 url('https://images.unsplash.com/photo-1535868463750-c78d9543614f?ixlib=rb-1.2.1&auto=format&fit=crop&w=1355&q=80') no-repeat center center fixed;
            background-size: cover;
            color: white;
            margin: 0;
            padding: 15px;
            display: flex;
            justify-content: center;
            align-items: flex-start;
            min-height: 100vh;
        }

        .container {
            background: rgba(10, 10, 10, 0.90);
            width: 100%;
            max-width: 400px;
            padding: 25px;
            border-radius: 25px;
            backdrop-filter: blur(20px);
            -webkit-backdrop-filter: blur(20px);
            border: 1px solid rgba(255,255,255,0.08);
            box-shadow: 0 20px 50px rgba(0,0,0,0.8);
            margin-top: 10px;
        }

        h1 { 
            color: #2ecc71; 
            text-align: center; 
            font-size: 28px; 
            margin-bottom: 25px; 
            font-weight: 800;
            letter-spacing: 1px;
            text-shadow: 0 0 10px rgba(46, 204, 113, 0.3);
        }

        input, select {
            width: 100%;
            height: 55px;
            padding: 12px 15px;
            border-radius: 16px;
            border: 2px solid #333;
            font-size: 17px;
            margin-bottom: 12px;
            background: #f5f5f5;
            color: #000;
            outline: none;
            font-weight: 600;
        }

        input:focus, select:focus { border-color: #2ecc71; }

        button {
            width: 100%;
            height: 55px;
            border-radius: 16px;
            border: none;
            font-weight: 800;
            font-size: 19px;
            cursor: pointer;
            margin-bottom: 12px;
            transition: all 0.2s;
            box-shadow: 0 5px 0 rgba(0,0,0,0.2);
        }

        button:active { transform: translateY(3px); box-shadow: none; }

        .add-btn { background: #27ae60; color: white; }
        .start-btn { background: #e67e22; color: white; margin-top: 15px; }
        .reset-btn { background: #c0392b; color: white; margin-top: 25px; }
        .next-btn { background: #3498db; color: white; }

        /* لیست */
        .player-list { 
            background: rgba(255,255,255,0.08); 
            border-radius: 16px; 
            margin-bottom: 15px; 
            max-height: 200px; 
            overflow-y: auto; 
            border: 1px solid rgba(255,255,255,0.05);
        }

        .player-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 14px 18px;
            border-bottom: 1px solid rgba(255,255,255,0.05);
            font-size: 17px;
            font-weight: 500;
        }

        .delete-icon { 
            color: #ff4757; 
            font-weight: bold; 
            padding: 5px; 
            cursor: pointer;
            font-size: 22px;
        }

        /* کارت */
        .card-display {
            background: #f1c40f;
            color: #2c3e50;
            min-height: 220px;
            border-radius: 25px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            margin: 30px 0;
            text-align: center;
            padding: 20px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.4);
            cursor: pointer;
            transition: transform 0.1s;
        }
        
        .card-display:active { transform: scale(0.98); }

        .word-ku { font-size: 36px; font-weight: 900; margin-bottom: 10px; line-height: 1.2; }
        .word-en { font-size: 20px; font-weight: 500; opacity: 0.8; font-family: sans-serif; letter-spacing: 0.5px; }
        
        .hidden { display: none !important; }
    </style>
</head>
<body>

<div class="container">
    <div id="setup-screen">
        <h1>🕵️‍♂️ یارییا خائین</h1>
        
        <select id="category-select">
            <option value="Random">🎲 هەمی تێکەل (Random - Best)</option>
            <option value="کەسایەتی">👤 کەسایەتی و هاڤال</option>
            <option value="تەپاپێ">⚽ تەپاپێ (Football)</option>
            <option value="تشتێن_ناڤمال">🏠 تشتێن مالێ (Home)</option>
            <option value="خوارن">🍔 خوارن (Food)</option>
            <option value="ئاژەڵ">🦁 ئاژەڵ (Animals)</option>
            <option value="باژێر">🌍 باژێر و وەڵات (Places)</option>
            <option value="تڕۆمبێل">🚗 تڕۆمبێل (Cars)</option>
            <option value="کار">🛠️ کار و پیشە (Jobs)</option>
            <option value="تەکنەلۆژیا">📱 تەکنەلۆژیا (Tech)</option>
            <option value="جلوبەرگ">👕 جلوبەرگ (Clothes)</option>
            <option value="سروشت">🌳 سروشت (Nature)</option>
        </select>

        <div style="display: flex; gap: 10px;">
            <input type="text" id="player-name" placeholder="ناڤێ یاریزانی..." enterkeyhint="done" style="margin-bottom: 0;">
            <button type="button" class="add-btn" id="add-btn-id" style="width: 80px; margin-bottom: 0;">+</button>
        </div>
        <p style="font-size: 13px; color: #888; margin-top: 8px; text-align: right;">ناڤێ بنڤیسە و پاشێ (+) لێ بدە</p>

        <div id="player-list-ui" class="player-list"></div>
        
        <button id="start-btn" class="start-btn hidden">دەستپێکرن ▶️</button>
    </div>

    <div id="game-screen" class="hidden">
        <h2 id="turn-name" style="color: #f1c40f; text-align: center; font-size: 26px;"></h2>
        <p style="text-align: center; opacity: 0.7; font-size: 15px; margin-top: -10px;">مۆبایلێ بدە ڤی کەسی و کلیک ل کارتێ بکە</p>
        
        <div id="card" class="card-display">
            <span class="word-ku">نیشان بدە 👁️</span>
        </div>
        
        <button id="next-player-btn" class="next-btn hidden">یێ دی لێ بدەت ⏭️</button>
        
        <div id="finish-area" class="hidden">
            <h3 style="color:#2ecc71; text-align:center; font-size: 28px;">هەمییان دیت! ✅</h3>
            <p style="text-align: center; color: #bbb; margin-bottom: 20px;">نۆکە دەست ب گەنگەشێ بکەن...</p>
            <button class="reset-btn" id="reset-btn-id">دوبارە یاری بکە 🔄</button>
        </div>
    </div>
</div>

<script>
    /* داتابەیسا "ئینفینیتی" - گەلەکا مەزنە
       Format: "Badini|English"
    */
    const rawData = {
        "کەسایەتی": [
            // هاڤالێن تە (Special Request)
            "سیداد|Sidad", "ئاماد|Amad", "ئەیاد|Ayad", "عمران|Imran", "ڕەیان|Rayan",
            // کەسایەتیێن جیهانی
            "Messi|Messi", "Ronaldo|Ronaldo", "Neymar|Neymar", "Elon Musk|Elon Musk", "The Rock|The Rock", 
            "Khabib|Khabib", "Jackie Chan|Jackie Chan", "MrBeast|MrBeast", "Spider-Man|Spider-Man", "Batman|Batman", 
            "Superman|Superman", "Iron Man|Iron Man", "Tom Cruise|Tom Cruise", "Justin Bieber|Justin Bieber", "Eminem|Eminem", 
            "Conor McGregor|Conor McGregor", "Mike Tyson|Mike Tyson", "Muhammad Ali|Muhammad Ali", "Bruce Lee|Bruce Lee", 
            "Donald Trump|Donald Trump", "Joe Biden|Joe Biden", "Putin|Putin", "Zelensky|Zelensky", "Kim Jong Un|Kim Jong Un", 
            "Barack Obama|Obama", "Mr. Bean|Mr. Bean", "Steve Jobs|Steve Jobs", "Bill Gates|Bill Gates", "Mark Zuckerberg|Mark Zuckerberg",
            "Johnny Depp|Johnny Depp", "Will Smith|Will Smith", "Harry Potter|Harry Potter", "John Wick|John Wick", "Undertaker|Undertaker", 
            "John Cena|John Cena", "Mario|Mario", "SpongeBob|SpongeBob", "Tom & Jerry|Tom & Jerry", "Joker|Joker", "Deadpool|Deadpool",
            "Thor|Thor", "Captain America|Captain America", "Hulk|Hulk", "Thanos|Thanos", "Michael Jackson|Michael Jackson", "Shakira|Shakira",
            "Adele|Adele", "Saddam Hussein|Saddam Hussein", "Adolf Hitler|Hitler", "Einstein|Einstein", "Tesla|Nikola Tesla", "Edison|Thomas Edison",
            "Cillian Murphy|Cillian Murphy", "Barbie|Barbie", "Oppenheimer|Oppenheimer", "Naruto|Naruto", "Goku|Goku", "Luffy|Luffy"
        ],
        "تەپاپێ": [
            "Messi|Messi", "Ronaldo|Ronaldo", "Neymar|Neymar", "Mbappe|Mbappe", "Haaland|Haaland", "Salah|Salah", "Benzema|Benzema", "Vinicius|Vinicius",
            "Bellingham|Bellingham", "Lewandowski|Lewandowski", "Lamine Yamal|Lamine Yamal", "Pedri|Pedri", "Gavi|Gavi", "De Bruyne|De Bruyne", 
            "Harry Kane|Harry Kane", "Neuer|Neuer", "Ter Stegen|Ter Stegen", "Courtois|Courtois", "Alisson|Alisson", "Ederson|Ederson", "Modric|Modric",
            "Kroos|Kroos", "Ramos|Ramos", "Zidane|Zidane", "Maradona|Maradona", "Pele|Pele", "Ronaldinho|Ronaldinho", "R9|Ronaldo Nazario",
            "Beckham|Beckham", "Xavi|Xavi", "Iniesta|Iniesta", "Buffon|Buffon", "Casillas|Casillas", "Ibrahimovic|Zlatan", "Rooney|Rooney",
            "Real Madrid|Real Madrid", "Barcelona|Barcelona", "Man City|Man City", "Liverpool|Liverpool", "Bayern Munich|Bayern Munich", 
            "PSG|PSG", "Man United|Man United", "Arsenal|Arsenal", "Chelsea|Chelsea", "Juventus|Juventus", "AC Milan|AC Milan", "Inter Milan|Inter Milan", "Dortmund|Dortmund",
            "نادی زاخۆ|Zakho SC", "نادی دهۆک|Duhok SC", "نادی هەولێر|Erbil SC", "هەڵبژاردێ عیراقێ|Iraq National Team", "هەڵبژاردێ بەرازیل|Brazil", 
            "هەڵبژاردێ ئەرجەنتین|Argentina", "هەڵبژاردێ ئەڵمانیا|Germany", "هەڵبژاردێ فەرەنسا|France", "هەڵبژاردێ ئیسپانیا|Spain", "هەڵبژاردێ ئیتالیا|Italy",
            "گۆڵچی|Goalkeeper", "حەکەم|Referee", "یاریگەهـ|Stadium", "کۆپا ئەمریکا|Copa America", "مۆندیال|World Cup", "ئۆفساید|Offside", 
            "پەنالتی|Penalty", "کۆرنەر|Corner", "کارتا سۆر|Red Card", "کارتا زەر|Yellow Card", "ڕاهێنەر|Coach", "تەپا پێ|Ball", "فیکە|Whistle",
            "گۆڵ|Goal", "دەقیقا ۹۰|90th Minute", "تەپا دەستی|Handball", "کاپتن|Captain", "خولا ئیسپانیا|La Liga", "خولا ئینگلیزی|Premier League"
        ],
        "تشتێن_ناڤمال": [
            "کورسی|Chair", "مێز|Table", "تەلەفزیۆن|TV", "سەلاجە|Fridge", "سپلیت|AC", "پەردە|Curtain", "کەوچک|Spoon", "چەتاڵ|Fork", 
            "قاپ|Plate", "پەرداخ|Glass", "مەنجەڵ|Pot", "فڕن|Oven", "غەسالە|Washing Machine", "جارۆکە|Broom", "کۆمپیوتەر|Computer", 
            "مۆبایل|Mobile", "ئێستیکان|Tea Glass", "بەتانی|Blanket", "بۆری|Pipe", "ئاڤدەست|Toilet", "دەوشەک|Mattress", "پێنجەرە|Window", 
            "دەرگەهـ|Door", "خەلات|Mixer", "مەکتەبە|Bookshelf", "سۆپا|Heater", "پانیکە|Fan", "شەحن|Charger", "هێدفۆن|Headphones", 
            "کلیل|Key", "قوفڵ|Lock", "چەرخ|Lighter", "خاولی|Towel", "سابین|Soap", "شامپۆ|Shampoo", "تەشت|Basin", "سەتڵ|Bucket", 
            "چەکوچ|Hammer", "بڕغی|Screw", "دەزی|Thread", "دەرزیک|Needle", "مەقەست|Scissors", "ئاوێنە|Mirror", "شانە|Comb", 
            "فێر|Hair Iron", "مکینا تراشێ|Shaver", "گڵۆپ|Bulb", "وایفای|Wi-Fi Router", "سەبەتە|Basket", "زەنگ|Bell", "تەخت|Bed",
            "بالیف|Pillow", "مافور|Carpet", "سقف|Ceiling", "دیوار|Wall", "پلاک|Socket", "وایر|Wire", "مێزا نانخوارنێ|Dining Table",
            "کەوەنتەر|Cupboard", "تەباخ|Stove", "چایدان|Teapot", "کتری|Kettle", "سینی|Tray", "دەرنەفیز|Screwdriver", "مەنجەلا بخارێ|Pressure Cooker"
        ],
        "خوارن": [
            "یاپراخ|Dolma", "کفتە|Kufta", "پیزا|Pizza", "بەرگر|Burger", "بریانی|Biryani", "کباب|Kebab", "ساڤار|Bulgur", "شۆربە|Soup", 
            "شیش کباب|Shish Kebab", "فەلافل|Falafel", "مەقەلۆبە|Maqluba", "برنج|Rice", "ماسیا برژى|Grilled Fish", "مریشک|Chicken", 
            "پەتاتە|Potato", "زەڵاتە|Salad", "ماست|Yogurt", "کولا|Cola", "چای|Tea", "قەهوە|Coffee", "ئاڤ|Water", "دۆلمە|Dolma", 
            "سەر و پێ|Pacha", "باجلە|Broad Beans", "نیسک|Lentils", "نۆک|Chickpeas", "لۆبی|Beans", "قەلی|Fried Meat", "تەشریب|Tashreeb", 
            "ئیندوومی|Indomie", "مەعکەرۆنی|Pasta", "شامی|Watermelon", "باقلاوە|Baklava", "کولێچە|Kleicha", "کێک|Cake", "دۆندرمە|Ice Cream", 
            "هەنار|Pomegranate", "سێڤ|Apple", "تڕی|Grapes", "خەیار|Cucumber", "تەماتە|Tomato", "پیڤاز|Onion", "سیر|Garlic", "نان|Bread", 
            "هێک|Egg", "پەنیر|Cheese", "کەرە|Butter", "موز|Banana", "پرتەقال|Orange", "لەیمون|Lemon", "فراولە|Strawberry", "گێلاس|Cherry",
            "خوێ|Salt", "شەکر|Sugar", "بیبەر|Pepper", "زەیتوون|Olive", "خورمە|Date", "گوێز|Walnut", "باوی|Almond", "فستەق|Pistachio",
            "ترشی|Pickles", "دوشاڤ|Syrup", "رەژو|Charcoal (BBQ)", "شربەت|Juice", "پەپسی|Pepsi", "سەفەر|Dining Table (Sheet)", "کوتلک|Kutilk", 
            "شەلەم|Turnip", "گازۆ|Cashews", "چپس|Chips", "نستەلە|Chocolate", "بسکیت|Biscuit", "حەلاوە|Halva", "مەحشی|Stuffed Veggies"
        ],
        "ئاژەڵ": [
            "شێر|Lion", "پڵنگ|Tiger", "فیل|Elephant", "کەرۆشک|Rabbit", "پێشی|Cat", "سە|Dog", "ئەسپ|Horse", "میمیک|Monkey", "کێسەل|Turtle", 
            "مار|Snake", "گورگ|Wolf", "رێڤی|Fox", "ورچ|Bear", "چێڵ|Cow", "بزن|Goat", "مەهـ|Sheep", "کەڵەشێر|Rooster", "کەفۆک|Pigeon", 
            "دایناسۆر|Dinosaur", "نەهەنگ|Whale", "قورقورک|Frog", "پەز|Sheep", "مریشک|Hen", "مێش|Fly", "پێسی|Mosquito", "زەرافە|Giraffe", 
            "کەنگەر|Kangaroo", "تیمساح|Crocodile", "قرژال|Crab", "عەقرەب|Scorpion", "هەسپێ ئاڤێ|Hippo", "کەر|Donkey", "هێشتر|Camel", 
            "کوچک|Puppy", "پاق|Duck", "قەل|Turkey", "چەقەل|Jackal", "مایین|Mare", "بالندە|Bird", "کەو|Partridge", "باز|Falcon", 
            "کوتر|Dove", "مێری|Ant", "پەپوولە|Butterfly", "زێبە|Zebra", "گەرگەدەن|Rhino", "قرش|Shark", "دۆلفین|Dolphin", "ئەختەبوت|Octopus",
            "حەسپێس|Spider", "مێشا هەنگڤینی|Bee", "کرم|Worm", "بۆق|Frog", "پاندا|Panda", "کوێلا|Koala", "سمۆرە|Squirrel", "ژژک|Hedgehog",
            "مشک|Mouse", "لەق لەق|Stork", "تیتک|Chick", "تەیر|Bird"
        ],
        "باژێر": [
            "دهۆک|Duhok", "هەولێر|Erbil", "سلێمانی|Sulaymaniyah", "زاخۆ|Zakho", "ئامێدی|Amedi", "ئاکرێ|Akra", "بەغدا|Baghdad", 
            "کەرکوک|Kirkuk", "ئیستەنبوڵ|Istanbul", "دوبای|Dubai", "پاریس|Paris", "لەندەن|London", "نیویۆرک|New York", "مەککە|Mecca", 
            "مەدینە|Medina", "ئەڵمانیا|Germany", "تورکیا|Turkey", "ئەمریکا|USA", "کوردستان|Kurdistan", "بەرازیل|Brazil", "ئەرجەنتین|Argentina", 
            "شێلادزێ|Sheladze", "سێمێل|Semel", "سۆران|Soran", "هەڵەبجە|Halabja", "موسڵ|Mosul", "بەسرە|Basra", "چین|China", "یابان|Japan", 
            "ڕوسیا|Russia", "کەنەدا|Canada", "ئوسترالیا|Australia", "هندستان|India", "میسر|Egypt", "بەردەرەش|Bardarash", "شەقلاوە|Shaqlawa", 
            "بەحرکە|Bahrka", "رۆما|Rome", "بەرلین|Berlin", "تۆکیۆ|Tokyo", "مەسکەو|Moscow", "ئیسپانیا|Spain", "ئیتالیا|Italy", "فەرەنسا|France",
            "سعودیە|Saudi Arabia", "کوێت|Kuwait", "ئیران|Iran", "سوریا|Syria", "لوبنان|Lebanon", "قەتەر|Qatar", "ئەوروپا|Europe", "ئاسیا|Asia",
            "رەواندز|Rawanduz", "کەلار|Kalar", "ڕانیە|Ranya"
        ],
        "تڕۆمبێل": [
            "BMW|BMW", "Mercedes|Mercedes", "Toyota|Toyota", "Nissan|Nissan", "Ford|Ford", "Hyundai|Hyundai", "Kia|Kia", "Land Cruiser|Land Cruiser", 
            "Hilux|Hilux", "Patrol|Patrol", "Sunny|Sunny", "Optima|Optima", "Elantra|Elantra", "Avalon|Avalon", "Camry|Camry", "G-Class|G-Class", 
            "Range Rover|Range Rover", "Ferrari|Ferrari", "Lamborghini|Lamborghini", "Bugatti|Bugatti", "Tesla|Tesla", "Jeep|Jeep", "Chevrolet|Chevrolet", 
            "تەکسى|Taxi", "پاس|Bus", "لۆری|Truck", "تڕێلە|Trailer", "ماتۆڕ|Motorcycle", "پایسکل|Bicycle", "تەیارە|Airplane", "قیتار|Train", 
            "کەشتی|Ship", "ئەمبۆلانس|Ambulance", "سەیارا پۆلیسا|Police Car", "شۆفڵ|Shovel", "ڕافیعە|Forklift", "تایەر|Tire", "گێڕ|Gear", 
            "ئیستۆپ|Brake", "بەزین|Petrol", "غاز|Gas", "دیزڵ|Diesel", "گزۆز|Exhaust", "جام|Glass", "سکان|Steering Wheel", "هەلیکۆپتەر|Helicopter",
            "پیکەب|Pickup", "تراکتۆر|Tractor", "کرێن|Crane", "دەبابە|Tank", "مەکینە|Engine", "رۆن|Oil", "پەمپ|Pump", "باتری|Battery"
        ],
        "کار": [
            "دکتۆر|Doctor", "مامۆستا|Teacher", "ئەندازیار|Engineer", "پۆلیس|Police", "پێشمەرگە|Peshmerga", "ئاسایش|Security", "حەلاق|Barber", 
            "شۆفێر|Driver", "فیتەر|Mechanic", "وەستایێ کەهرەبێ|Electrician", "وەستایێ خانیێ|Builder", "پارێزەر|Lawyer", "دادوەر|Judge", 
            "بازرگان|Businessman", "فرۆشیار|Seller", "نەجار|Carpenter", "خەیات|Tailor", "نانپێژ|Baker", "قەساب|Butcher", "فڕۆکەڤان|Pilot", 
            "یاریزان|Player", "رۆژنامەڤان|Journalist", "وەرزێڕ|Farmer", "ماسیگر|Fisherman", "ئاگرکوژ|Firefighter", "پەرستار|Nurse", 
            "دەرمانساز|Pharmacist", "فۆتۆگرافەر|Photographer", "شێف|Chef", "گارسۆن|Waiter", "وەرگێڕ|Translator", "نوڤیسەر|Writer", 
            "گۆرانیبێژ|Singer", "ئەکتەر|Actor", "مەڵا|Mullah", "سەرباز|Soldier", "رەسام|Painter", "سەرۆک|President", "وەزیر|Minister",
            "بەربەر|Barber", "کابرایێ دلیڤەری|Delivery Man", "پاسەوان|Guard", "خزمەتگوزار|Cleaner", "زێرینگر|Goldsmith", "بەقال|Grocer",
            "دکتۆرێ ددانا|Dentist"
        ],
        "تەکنەلۆژیا": [
            "لاپتۆپ|Laptop", "ئایپاد|iPad", "تەباخ|Stove", "پلایستەیشن|PlayStation", "ئێکس بۆکس|Xbox", "ماوس|Mouse", "کیبۆرد|Keyboard", 
            "فلاش|Flash Drive", "هارد|Hard Drive", "کامیرە|Camera", "درۆن|Drone", "ڕۆبۆت|Robot", "سەتەلایت|Satellite", "ڕادێۆ|Radio", 
            "باتری|Battery", "وایەر|Wire", "پلاک|Plug", "سێرڤەر|Server", "ئینتەرنێت|Internet", "شاشە|Screen", "مایکرۆفۆن|Microphone", 
            "دەنگ|Sound", "بلوتوث|Bluetooth", "سیمکارت|SIM Card", "تەبرید|Air Cooler", "گڵۆپ|Light Bulb", "سویچ|Switch", "مۆدێم|Modem",
            "تەلەفۆن|Telephone", "سەماعە|Speaker", "پرێنتەر|Printer"
        ],
        "جلوبەرگ": [
             "قەمسەلە|Jacket", "پانتۆڵ|Trousers", "تیشێرت|T-Shirt", "کراس|Shirt", "شەروال|Kurdish Pants", "جلی کوردی|Kurdish Clothes",
             "کەڤوک|Coat", "پێلاڤ|Shoes", "نەعال|Slippers", "گۆرە|Socks", "کڵاڤ|Hat", "شەبکە|Cap", "پشتێن|Belt", "سەعەت|Watch",
             "چاڤیلکە|Glasses", "ملپێچ|Scarf", "دەستکێش|Gloves", "بیجامە|Pajamas", "شۆرت|Shorts", "بەرگ|Suit", "کراسێ خەوێ|Sleepwear",
             "بوت|Boots", "جزدان|Wallet", "جانتا|Bag", "زێر|Gold", "زیڤ|Silver", "ئەلقە|Ring"
        ],
        "سروشت": [
            "چیایێ گارە|Gara Mountain", "چیایێ مەتین|Mateen Mountain", "ڕووبار|River", "دەریا|Sea", "ئەسمان|Sky", "هەیڤ|Moon", "ڕۆژ|Sun",
            "ستێرک|Star", "عەور|Cloud", "باران|Rain", "بەفر|Snow", "تەزرە|Hail", "با|Wind", "تۆز|Dust", "گژوگیا|Grass", "دار|Tree",
            "گوڵ|Flower", "بەرمای|Lake", "بیابان|Desert", "دارستان|Forest", "ئاڤ|Water", "خوێ|Sand", "بەڤر|Ice", "ئاگر|Fire",
            "دویکێل|Smoke", "خاڕ|Soil", "بەر|Stone", "شکەفت|Cave", "سێلاڤ|Waterfall", "قەوسەقەزەح|Rainbow"
        ]
    };

    let players = [];
    let gameData = { imposterIndex: -1, wordKu: "", wordEn: "", currentIndex: 0 };

    const addBtn = document.getElementById('add-btn-id');
    const inputField = document.getElementById('player-name');

    // 1. iPhone Fix for Buttons
    ['click', 'touchstart'].forEach(evt => {
        addBtn.addEventListener(evt, function(e) {
            if(e.cancelable && evt === 'touchstart') e.preventDefault(); 
            if(evt === 'click' || evt === 'touchstart') addPlayerLogic();
        }, {passive: false});
    });

    inputField.addEventListener("keypress", function(event) {
        if (event.key === "Enter") {
            event.preventDefault();
            addPlayerLogic();
        }
    });

    function addPlayerLogic() {
        const name = inputField.value.trim();
        if (name) {
            players.push(name);
            inputField.value = "";
            renderPlayers();
            inputField.focus();
        }
    }

    function renderPlayers() {
        const list = document.getElementById('player-list-ui');
        list.innerHTML = players.map((p, i) => `
            <div class="player-item">
                <span>${i + 1}. ${p}</span>
                <span class="delete-icon" onclick="removePlayer(${i})">✖</span>
            </div>
        `).join('');
        
        const startBtn = document.getElementById('start-btn');
        if (players.length >= 3) {
            startBtn.classList.remove('hidden');
        } else {
            startBtn.classList.add('hidden');
        }
    }

    window.removePlayer = function(i) {
        players.splice(i, 1);
        renderPlayers();
    };

    // 2. Game Logic
    document.getElementById('start-btn').addEventListener('click', function() {
        const cat = document.getElementById('category-select').value;
        let list = [];
        
        if (cat === "Random") {
            // Collect ALL words from ALL categories
            Object.values(rawData).forEach(arr => list.push(...arr));
        } else {
            list = rawData[cat];
        }
        
        // Pick a random word
        const rawSelection = list[Math.floor(Math.random() * list.length)];
        const splitWord = rawSelection.split('|');
        gameData.wordKu = splitWord[0];
        gameData.wordEn = splitWord[1];

        // Pick Imposter
        gameData.imposterIndex = Math.floor(Math.random() * players.length);
        gameData.currentIndex = 0;

        // UI Switch
        document.getElementById('setup-screen').classList.add('hidden');
        document.getElementById('game-screen').classList.remove('hidden');
        document.getElementById('finish-area').classList.add('hidden');
        
        showTurn();
    });

    function showTurn() {
        document.getElementById('turn-name').innerText = "نۆکا ( " + players[gameData.currentIndex] + " )";
        const card = document.getElementById('card');
        card.innerHTML = '<span class="word-ku" style="font-size:28px">نیشان بدە 👁️</span>';
        card.style.background = "#f1c40f";
        card.style.color = "#2c3e50";
        document.getElementById('next-player-btn').classList.add('hidden');
    }

    document.getElementById('card').addEventListener('click', function() {
        const card = this;
        // Prevent double click if already shown
        if (card.style.background === "rgb(231, 76, 60)" || card.style.background === "rgb(46, 204, 113)") return;

        if (gameData.currentIndex === gameData.imposterIndex) {
            card.innerHTML = `
                <span class="word-ku" style="font-size:32px">🤫 تو خائینی!</span>
                <span class="word-en">(You are the Imposter)</span>
            `;
            card.style.background = "#e74c3c"; 
            card.style.color = "white";
        } else {
            card.innerHTML = `
                <span class="word-ku">${gameData.wordKu}</span>
                <span class="word-en">(${gameData.wordEn})</span>
            `;
            card.style.background = "#2ecc71"; 
            card.style.color = "white";
        }
        
        if (gameData.currentIndex < players.length - 1) {
            document.getElementById('next-player-btn').classList.remove('hidden');
        } else {
            document.getElementById('finish-area').classList.remove('hidden');
        }
    });

    document.getElementById('next-player-btn').addEventListener('click', function() {
        gameData.currentIndex++;
        showTurn();
    });

    document.getElementById('reset-btn-id').addEventListener('click', function() {
        document.getElementById('game-screen').classList.add('hidden');
        document.getElementById('setup-screen').classList.remove('hidden');
        // Reset game data but KEEP players array
        gameData.imposterIndex = -1;
        gameData.wordKu = "";
        gameData.wordEn = "";
        gameData.currentIndex = 0;
    });

</script>

</body>
</html>
