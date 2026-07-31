[index.html.html](https://github.com/user-attachments/files/30585714/index.html.html)
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>清蓝多功能工作台</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: system-ui, -apple-system, "Microsoft YaHei", sans-serif;
        }
        /* 全局蓝白色系，全程无黑色 */
        :root {
            --sky-blue: #67C6E3;    /* 天蓝 */
            --deep-blue: #2474B3;   /* 深蓝文字 */
            --light-white-blue: #F8FCFF; /* 极浅白蓝 */
            --light-blue: #DFF5FF;  /* 浅蓝分区 */
            --mid-blue: #429ED7;    /* 中度蓝 */
            --white: #ffffff;
            --line-blue: #b8e3f2;
        }
        body {
            background: linear-gradient(140deg, #E6F7FF 0%, #F5FCFF 100%);
            color: var(--deep-blue);
            padding: 40px 20px;
            min-height: 100vh;
            overflow-x: hidden;
            position: relative;
        }
        /* 背景柔光美化 */
        body::before {
            content: "";
            position: fixed;
            width: 300px;
            height: 300px;
            border-radius: 50%;
            background: radial-gradient(circle, rgba(103, 198, 227, 0.12) 0%, transparent 70%);
            top: -100px;
            left: -80px;
            z-index: -1;
        }
        body::after {
            content: "";
            position: fixed;
            width: 400px;
            height: 400px;
            border-radius: 50%;
            background: radial-gradient(circle, rgba(66, 158, 215, 0.08) 0%, transparent 70%);
            bottom: -150px;
            right: -120px;
            z-index: -1;
        }
        .container {
            max-width: 1100px;
            margin: 0 auto;
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 26px;
        }
        .card {
            background: var(--white);
            padding: 24px;
            border-radius: 14px;
            border: 1px solid var(--line-blue);
            transition: all 0.3s ease;
            box-shadow: 0 2px 8px rgba(103, 198, 227, 0.06);
            position: relative;
            overflow: hidden;
        }
        .card::before {
            content: "";
            position: absolute;
            width: 100%;
            height: 3px;
            background: linear-gradient(90deg, var(--sky-blue), var(--mid-blue));
            top: 0;
            left: 0;
        }
        .card:hover {
            background: #f8fbff;
            transform: translateY(-4px);
            box-shadow: 0 6px 16px rgba(103, 198, 227, 0.16);
        }
        .card-full {
            grid-column: 1 / -1;
        }
        h3 {
            font-size: 18px;
            margin-bottom: 18px;
            color: var(--deep-blue);
            font-weight: 600;
            display: flex;
            justify-content: space-between;
            align-items: center;
            letter-spacing: 1px;
        }
        button {
            background: linear-gradient(135deg, var(--sky-blue), var(--mid-blue));
            border: none;
            color: var(--white);
            padding: 8px 15px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 13px;
            transition: all 0.25s;
            font-weight: 500;
        }
        button:hover {
            background: linear-gradient(135deg, var(--mid-blue), var(--deep-blue));
            transform: scale(1.04);
        }
        button.danger {
            background: linear-gradient(135deg, #f28c8c, #e06868);
        }
        button.danger:hover {
            background: linear-gradient(135deg, #e06868, #c84e4e);
        }
        input, select {
            border: 1px solid var(--line-blue);
            padding: 9px 12px;
            border-radius: 8px;
            outline: none;
            font-size: 14px;
            background: #fafcff;
            transition: border 0.25s, box-shadow 0.25s;
        }
        input:focus {
            border-color: var(--mid-blue);
            box-shadow: 0 0 0 3px rgba(66, 158, 215, 0.15);
            background: #fff;
        }
        /* 时间模块 */
        .time-box {
            text-align: center;
        }
        #nowTime {
            font-size: 48px;
            font-weight: 600;
            letter-spacing: 4px;
            color: var(--deep-blue);
        }
        #nowDate {
            font-size: 20px;
            margin-top: 10px;
            opacity: 0.9;
            font-weight: 500;
        }
        #dayCountdown {
            margin-top: 8px;
            font-size: 14px;
            color: var(--mid-blue);
        }
        .day-progress {
            width: 100%;
            height: 7px;
            background: var(--light-blue);
            border-radius: 4px;
            margin-top: 12px;
            overflow: hidden;
        }
        .progress-bar {
            height: 100%;
            background: linear-gradient(90deg, var(--sky-blue), var(--mid-blue));
            border-radius: 4px;
            transition: width 1s linear;
        }
        /* 待办清单 */
        .todo-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 12px 0;
            border-bottom: 1px dashed var(--line-blue);
        }
        .todo-add {
            display: flex;
            gap: 10px;
            margin-bottom: 14px;
            flex-wrap: wrap;
        }
        /* 书签图标区域 */
        .bookmark-wrap {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 14px;
        }
        .book-item a {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap:8px;
            text-align: center;
            padding: 14px 8px;
            background: var(--light-white-blue);
            text-decoration: none;
            color: var(--deep-blue);
            border-radius: 10px;
            font-size: 14px;
            transition: all 0.25s;
        }
        .book-item img {
            width:36px;
            height:36px;
            object-fit:cover;
            border-radius:8px;
        }
        .book-item a:hover {
            background: var(--sky-blue);
            color: white;
            transform: translateY(-3px);
        }
        /* 天气模块 */
        .weather-info {
            font-size: 14px;
            line-height: 1.9;
        }
        .weather-row {
            display: flex;
            gap: 10px;
            margin-bottom: 12px;
            flex-wrap: wrap;
        }
        .weather-card {
            border:1px solid var(--line-blue);
            padding:14px;
            border-radius:10px;
            margin-bottom:10px;
            background: #fcfefe;
        }
        .weather-label {
            font-weight:600;
            color:var(--deep-blue);
        }
        /* 语录 */
        #quoteCn {
            font-weight:600;
            font-size:17px;
            color: var(--deep-blue);
            margin-bottom:10px;
        }
        #quoteEn {
            font-size:15px;
            margin-bottom:8px;
            color:#336088;
        }
        #quoteSource {
            font-size:14px;
            color:#557a99;
        }
        .quote-buttons {
            margin-top: 14px;
            display: flex;
            gap: 12px;
        }
        /* 汇率 */
        .rate-list {
            font-size: 14px;
            line-height: 2;
        }
        .rate-input {
            margin-bottom: 12px;
            display: flex;
            gap: 10px;
            align-items: center;
        }
        /* 转盘 蓝白专用样式 */
        .turntable-box {
            text-align: center;
            position: relative;
        }
        .wheel-pointer {
            position: absolute;
            top: 0;
            left: 50%;
            transform: translateX(-50%);
            width: 0;
            height: 0;
            border-left: 14px solid transparent;
            border-right: 14px solid transparent;
            border-top: 24px solid var(--deep-blue);
            z-index: 9;
        }
        #wheelCanvas {
            width: 270px;
            height: 270px;
            margin: 12px auto;
            border-radius: 50%;
            display: block;
            border: 4px solid var(--sky-blue);
            background: #fff;
            position: relative;
            transform-origin: center center;
        }
        .option-inputs {
            margin: 14px 0;
            max-height: 160px;
            overflow-y: auto;
            padding-right: 6px;
        }
        .option-item {
            display: flex;
            gap: 10px;
            margin: 8px 0;
        }
        #wheelResult {
            margin-top:14px;
            font-weight:bold;
            font-size:17px;
            color:var(--deep-blue);
        }
        /* 底部工具 */
        .global-tool {
            max-width: 1100px;
            margin: 34px auto 0;
            text-align: center;
            display: flex;
            gap: 14px;
            justify-content: center;
            flex-wrap: wrap;
        }
    </style>
</head>
<body>
    <!-- 已彻底移除鲸鱼、所有海洋动态元素 -->
    <div class="container">
        <!-- 实时时间 -->
        <div class="card time-box">
            <h3>此刻时间 <span id="fullScreenBtn"><button onclick="toggleFull()">全屏</button></span></h3>
            <div id="nowTime">00:00:00</div>
            <div id="nowDate">2026年07月31日 星期五</div>
            <div id="dayCountdown">距离今日结束：00:00:00</div>
            <div class="day-progress">
                <div class="progress-bar" id="dayBar"></div>
            </div>
        </div>
        <!-- 天气 -->
        <div class="card">
            <h3>实时天气 <button onclick="addWeatherWidget()">添加城市小组件</button></h3>
            <div class="weather-info" id="weatherWrap"></div>
        </div>
        <!-- 待办 -->
        <div class="card">
            <h3>待办清单</h3>
            <div class="todo-add">
                <input id="todoText" placeholder="任务内容">
                <input id="todoTime" type="datetime-local">
                <button onclick="addTodo()">新增</button>
            </div>
            <div id="todoList"></div>
        </div>
        <!-- 快捷书签（带软件图标） -->
        <div class="card">
            <h3>快捷书签</h3>
            <div class="bookmark-wrap" id="bookWrap"></div>
        </div>
        <!-- 语录通栏 -->
        <div class="card card-full">
            <h3>今日哲理语录</h3>
            <div id="quoteCn"></div>
            <div id="quoteEn"></div>
            <div id="quoteSource"></div>
            <div class="quote-buttons">
                <button onclick="randomQuote()">换一句</button>
                <button onclick="collectQuote()">收藏本条</button>
                <button onclick="showCollect()">查看收藏</button>
            </div>
        </div>
        <!-- 汇率 -->
        <div class="card">
            <h3>人民币实时汇率</h3>
            <div class="rate-input">
                <span>换算金额：</span>
                <input id="rateNum" value="1" type="number" min="0.01" step="0.1" oninput="getRate()">
                <button onclick="getRate()">重新计算</button>
            </div>
            <div class="rate-list" id="rateBox">加载汇率...</div>
        </div>
        <!-- 蓝白转盘 -->
        <div class="card">
            <h3>随机选择转盘</h3>
            <div class="turntable-box">
                <div class="wheel-pointer"></div>
                <canvas id="wheelCanvas"></canvas>
            </div>
            <button onclick="startWheel()">转动转盘</button>
            <div class="option-inputs" id="optWrap"></div>
            <button onclick="addOption()">新增选项(最多20)</button>
            <div id="wheelResult"></div>
        </div>
    </div>
    <div class="global-tool">
        <button class="danger" onclick="clearAllData()">一键清空本地所有数据</button>
    </div>
<script>
// 本地存储工具
const Storage = {
    get(key) {
        let data = localStorage.getItem(key);
        return data ? JSON.parse(data) : null;
    },
    set(key, val) {
        localStorage.setItem(key, JSON.stringify(val));
    },
    remove(key) {
        localStorage.removeItem(key);
    },
    clearAll() {
        localStorage.clear();
    }
}
// 全屏切换
function toggleFull() {
    if (!document.fullscreenElement) document.documentElement.requestFullscreen();
    else document.exitFullscreen();
}
// 清空数据
function clearAllData() {
    if (!confirm("确定清空待办、书签、转盘、收藏、天气城市全部数据？不可恢复！")) return;
    Storage.clearAll();
    location.reload();
}
// 时间更新
function updateTime() {
    const now = new Date();
    const timeStr = now.toLocaleTimeString('zh-CN', {hour12:false});
    const dateStr = now.toLocaleDateString('zh-CN', {year:'numeric',month:'long',day:'numeric',weekday:'long'});
    document.getElementById('nowTime').innerText = timeStr;
    document.getElementById('nowDate').innerText = dateStr;
    const end = new Date();
    end.setHours(23,59,59,999);
    const diff = end - now;
    const h = Math.floor(diff / 3600000);
    const m = Math.floor((diff % 3600000)/60000);
    const s = Math.floor((diff % 60000)/1000);
    document.getElementById('dayCountdown').innerText = `距离今日结束：${String(h).padStart(2,'0')}:${String(m).padStart(2,'0')}:${String(s).padStart(2,'0')}`;
    const dayTotal = 24*3600*1000;
    const dayPass = now - new Date(now.setHours(0,0,0,0));
    const percent = (dayPass / dayTotal) * 100;
    document.getElementById('dayBar').style.width = `${percent}%`;
}
setInterval(updateTime, 1000);
updateTime();
// 待办清单
let todoList = Storage.get('todo') || [];
function renderTodo() {
    const wrap = document.getElementById('todoList');
    wrap.innerHTML = '';
    todoList.forEach((item, idx)=>{
        const div = document.createElement('div');
        div.className = 'todo-item';
        div.innerHTML = `
            <div>${item.text} <span style="opacity:0.7;font-size:12px;">${item.deadline || '无截止时间'}</span></div>
            <button onclick="delTodo(${idx})">删除</button>
        `;
        wrap.appendChild(div);
    })
}
function addTodo() {
    const text = document.getElementById('todoText').value.trim();
    const time = document.getElementById('todoTime').value;
    if(!text) return alert('请输入任务内容');
    todoList.push({text, deadline:time});
    Storage.set('todo', todoList);
    renderTodo();
    document.getElementById('todoText').value = '';
}
function delTodo(i) {
    todoList.splice(i,1);
    Storage.set('todo', todoList);
    renderTodo();
}
renderTodo();
// 书签 软件图标
const bookmarks = [
    {name:"夸克浏览器",url:"https://quark.sm.cn/",icon:"https://lf-cdn-tos.byteimg.com/obj/open-platform-img/quark_logo.png"},
    {name:"B站",url:"https://bilibili.com",icon:"https://lf-cdn-tos.byteimg.com/obj/open-platform-img/bilibili_logo.png"},
    {name:"微博",url:"https://weibo.com",icon:"https://lf-cdn-tos.byteimg.com/obj/open-platform-img/weibo_logo.png"},
    {name:"头条",url:"https://www.toutiao.com",icon:"https://lf-cdn-tos.byteimg.com/obj/open-platform-img/toutiao_logo.png"}
];
function renderBook() {
    const wrap = document.getElementById('bookWrap');
    wrap.innerHTML = '';
    bookmarks.forEach(item=>{
        const div = document.createElement('div');
        div.className = 'book-item';
        div.innerHTML = `
            <a href="${item.url}" target="_blank">
                <img src="${item.icon}" alt="${item.name}图标" loading="eager">
                <span>${item.name}</span>
            </a>
        `;
        wrap.appendChild(div);
    })
}
renderBook();
// 天气模块
let weatherCityList = Storage.get('weatherCity') || ['拉萨'];
const weatherIconMap = {
    "Clear": "☀️ 晴天","Sunny": "☀️ 晴天","Partly Cloudy": "⛅ 多云","Cloudy": "☁️ 阴天","Overcast": "☁️ 阴天","Rain": "🌧️ 下雨","Light rain": "🌦️ 小雨","Heavy rain": "⛈️ 大雨","Snow": "❄️ 下雪","Thunderstorm": "⛈️ 雷暴","Mist": "🌫️ 雾","Fog": "🌫️ 大雾"
};
function addWeatherWidget() {
    const city = prompt("请输入新增城市名称：");
    if(!city || city.trim() === "") return;
    const c = city.trim();
    if(weatherCityList.includes(c)) return alert("该城市已存在！");
    weatherCityList.push(c);
    Storage.set('weatherCity', weatherCityList);
    renderAllWeather();
}
function delWeatherCity(cityName) {
    weatherCityList = weatherCityList.filter(item => item !== cityName);
    Storage.set('weatherCity', weatherCityList);
    renderAllWeather();
}
async function renderAllWeather() {
    const wrap = document.getElementById('weatherWrap');
    wrap.innerHTML = "";
    for(const city of weatherCityList) {
        const card = document.createElement('div');
        card.className = "weather-card";
        card.innerHTML = `
            <div class="weather-row">
                <input value="${city}" placeholder="城市" onchange="updateSingleCity(this.value,'${city}')">
                <button onclick="refreshSingleWeather('${city}')">刷新</button>
                <button onclick="delWeatherCity('${city}')" class="danger">移除</button>
            </div>
            <div id="weather-${city}" style="color:#336088;">加载中...</div>
        `;
        wrap.appendChild(card);
        await loadSingleWeather(city);
    }
}
async function updateSingleCity(newCity, oldCity) {
    const idx = weatherCityList.findIndex(i=>i===oldCity);
    weatherCityList[idx] = newCity.trim();
    Storage.set('weatherCity', weatherCityList);
    renderAllWeather();
}
async function refreshSingleWeather(city) {
    await loadSingleWeather(city);
}
async function loadSingleWeather(city) {
    const box = document.getElementById(`weather-${city}`);
    if(!box) return;
    box.innerText = "正在获取天气...";
    try {
        const res = await fetch(`https://wttr.in/${city}?format=j1&lang=zh`);
        const data = await res.json();
        const curr = data.current_condition[0];
        let weatherText = curr.lang_zh?.[0]?.value || curr.weatherDesc[0].value;
        let icon = "";
        for(let key in weatherIconMap) {
            if(curr.weatherDesc[0].value.includes(key)) icon = weatherIconMap[key];
        }
        if(!icon) icon = "🌤️ 多云";
        const temp = curr.temp_C;
        const feel = curr.FeelsLikeC;
        const humidity = curr.humidity;
        const wind = curr.windspeedKmph;
        box.innerHTML = `
            <div><span class="weather-label">天气：</span>${icon} ${weatherText}</div>
            <div><span class="weather-label">温度：</span>${temp}℃，体感${feel}℃</div>
            <div><span class="weather-label">湿度：</span>${humidity}%</div>
            <div><span class="weather-label">风力：</span>${wind}km/h</div>
        `;
    }catch(err) {
        box.innerText = `城市「${city}」天气获取失败，请检查名称`;
    }
}
renderAllWeather();
// 语录模块
const quotePool = [
    {cn:"云雾会遮蔽神山，可光从未消失，等待不是煎熬，是等雾散去看清本心。",en:"Clouds may obscure the sacred mountain, yet light never fades. Waiting is not suffering, but a chance to see your true heart when mist clears.",source:"雪域禅语"},
    {cn:"心若澄澈，高原天光自会落满肩头。",en:"If your heart is pure, the plateau sunlight will rest gently upon your shoulders.",source:"藏地随笔"},
    {cn:"不必向外追逐光亮，向内自观，便自带圣光。",en:"You need not chase light outside yourself; look inward, and you carry your own radiance.",source:"心灵哲思"},
    {cn:"所有外界的光亮都是转瞬过客，真正的光根植于心。",en:"All light from the outside world passes fleetingly; true light grows deep within your soul.",source:"静心录"},
    {cn:"静守本心，云雾散尽，自有万丈雪域明光。",en:"Calmly guard your inner heart; when mist fades, boundless snowy radiance shall unfold.",source:"高原悟道"}
];
let collectQuotes = Storage.get('quoteCollect') || [];
let nowQuote = {};
function randomQuote() {
    nowQuote = quotePool[Math.floor(Math.random()*quotePool.length)];
    document.getElementById('quoteCn').innerText = nowQuote.cn;
    document.getElementById('quoteEn').innerText = nowQuote.en;
    document.getElementById('quoteSource').innerText = `出处：${nowQuote.source}`;
    Storage.set('lastQuote', nowQuote);
}
function collectQuote() {
    if(!nowQuote.cn) return;
    const exist = collectQuotes.some(q=>q.cn === nowQuote.cn);
    if(exist) return alert("本条已收藏！");
    collectQuotes.push(nowQuote);
    Storage.set('quoteCollect', collectQuotes);
    alert("收藏成功！");
}
function showCollect() {
    if(collectQuotes.length === 0) return alert("暂无收藏语录");
    let text = "收藏语录列表：\n\n";
    collectQuotes.forEach(q=>{
        text += `【${q.source}】\n${q.cn}\n${q.en}\n\n`;
    })
    alert(text);
}
randomQuote();
// 汇率换算
async function getRate() {
    const box = document.getElementById('rateBox');
    const num = Number(document.getElementById('rateNum').value) || 1;
    try {
        const res = await fetch('https://api.exchangerate-api.com/v4/latest/CNY');
        const data = await res.json();
        const list = [
            `美元 USD：${(num * data.rates.USD).toFixed(2)}`,
            `欧元 EUR：${(num * data.rates.EUR).toFixed(2)}`,
            `英镑 GBP：${(num * data.rates.GBP).toFixed(2)}`,
            `日元 JPY：${(num * data.rates.JPY).toFixed(2)}`,
            `港币 HKD：${(num * data.rates.HKD).toFixed(2)}`,
            `韩元 KRW：${(num * data.rates.KRW).toFixed(2)}`
        ]
        box.innerHTML = list.join('<br>');
    }catch(e) {
        box.innerText = "汇率加载失败，稍后重试";
    }
}
getRate();
// ====================== 转盘核心 蓝白配色 无黑色 ======================
let wheelOpts = Storage.get('wheelOpt') || ['休息','工作','看书','散步'];
const canvas = document.getElementById('wheelCanvas');
const ctx = canvas.getContext('2d');
canvas.width = 270;
canvas.height = 270;
let rotateDeg = 0;
let isSpinning = false;
// 严格蓝白三色，无任何黑色
const colorLightWhite = "#F8FCFF";  // 白调浅蓝
const colorLightBlue = "#DFF5FF";   // 浅蓝
const colorSkyBlue = "#67C6E3";     // 天蓝
const textColor = "#2474B3";        // 深蓝文字，不用黑色
function renderWheelOpt() {
    const wrap = document.getElementById('optWrap');
    wrap.innerHTML = '';
    wheelOpts.forEach((opt,idx)=>{
        const div = document.createElement('div');
        div.className = 'option-item';
        div.innerHTML = `
            <input value="${opt}" onchange="editOpt(${idx},this.value)">
            <button onclick="delOpt(${idx})">-</button>
        `;
        wrap.appendChild(div);
    })
    drawWheel();
}
function addOption() {
    if(wheelOpts.length >=20) return alert("最多只能添加20个选项");
    wheelOpts.push('新选项');
    Storage.set('wheelOpt', wheelOpts);
    renderWheelOpt();
}
function editOpt(i,val) {
    wheelOpts[i] = val;
    Storage.set('wheelOpt', wheelOpts);
    drawWheel();
}
function delOpt(i) {
    wheelOpts.splice(i,1);
    Storage.set('wheelOpt', wheelOpts);
    renderWheelOpt();
}
function drawWheel() {
    const w = canvas.width;
    const h = canvas.height;
    const radius = w / 2 - 14;
    ctx.clearRect(0,0,w,h);
    // 底层纯白色底盘，杜绝黑色底色
    ctx.fillStyle = "#ffffff";
    ctx.beginPath();
    ctx.arc(w/2, h/2, radius, 0, Math.PI * 2);
    ctx.fill();
    const segmentAngle = 360 / wheelOpts.length;
    // 循环三色交替，相邻区块颜色不同
    const colorArr = [colorLightWhite, colorLightBlue, colorSkyBlue];
    for(let i = 0; i < wheelOpts.length; i++) {
        const startDeg = segmentAngle * i - 90;
        const endDeg = segmentAngle * (i + 1) - 90;
        ctx.fillStyle = colorArr[i % colorArr.length];
        ctx.beginPath();
        ctx.moveTo(w/2, h/2);
        ctx.arc(w/2, h/2, radius, startDeg * Math.PI / 180, endDeg * Math.PI / 180);
        ctx.closePath();
        ctx.fill();
        // 分割线白色，无黑边
        ctx.strokeStyle = "#ffffff";
        ctx.lineWidth = 3;
        ctx.stroke();
        // 文字深蓝，无黑色
        ctx.save();
        ctx.translate(w/2, h/2);
        ctx.rotate((startDeg + segmentAngle / 2) * Math.PI / 180);
        ctx.fillStyle = textColor;
        ctx.font = "bold 16px Microsoft YaHei, sans-serif";
        ctx.fillText(wheelOpts[i], radius * 0.43, 6);
        ctx.restore();
    }
    // 中心小圆 天蓝
    ctx.fillStyle = colorSkyBlue;
    ctx.beginPath();
    ctx.arc(w/2, h/2, 10, 0, Math.PI * 2);
    ctx.fill();
}
// 仅修改此函数，指针定位精准匹配
function startWheel() {
    if(isSpinning) return;
    isSpinning = true;
    // 随机多圈旋转
    const randomCircle = 5 + Math.floor(Math.random() * 6);
    const targetExtra = Math.random() * 360;
    const targetRotate = rotateDeg + randomCircle * 360 + targetExtra;
    canvas.style.transition = 'transform 4s cubic-bezier(0.2,0,0.2,1)';
    canvas.style.transform = `rotate(${targetRotate}deg)`;
    rotateDeg = targetRotate;
    setTimeout(()=>{
        isSpinning = false;
        // 计算指针（顶部0度）对准的区块
        const totalRotate = rotateDeg % 360;
        const pointerAngle = (360 - totalRotate) % 360;
        const seg = 360 / wheelOpts.length;
        const selectIndex = Math.floor(pointerAngle / seg);
        document.getElementById('wheelResult').innerText = `选中结果：${wheelOpts[selectIndex]}`;
        Storage.set('lastWheelSelect', wheelOpts[selectIndex]);
    },4000);
}
renderWheelOpt();
drawWheel();
</script>
</body>
</html>
