<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>異星座標：靈魂與星座標分析</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+TC:wght@400;500;700;900&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Noto Sans TC', sans-serif; background-color: #eef2f7; }
        .fade-in { animation: fadeIn 0.5s ease-out; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
        .slide-up { animation: slideUp 0.7s ease-out; }
        @keyframes slideUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
    </style>
</head>
<body class="min-h-screen flex items-center justify-center p-4">

    <div id="app" class="w-full max-w-[500px] bg-white rounded-[40px] shadow-xl overflow-hidden p-8 md:p-10 text-center relative min-h-[600px] flex flex-col justify-center">
        <!-- 內容會由 JavaScript 動態插入 -->
    </div>

    <script>
        // --- 數據定義 ---
        const questions = [
            { q: "進入群體討論時，你扮演的角色通常是？", o: ["直播電台：第一個開口並主導討論方向", "收音設備：聽完大家想法後才給關鍵意見", "公關經理：在各個小組間傳話協調氣氛", "紀錄機器：默默記下重點並在腦中規劃"], d: ["E", "I", "E", "I"] },
            { q: "當你面對一個完全陌生的挑戰，你的直覺反應是？", o: ["先衝再說，在行動中尋找解決方案", "收集資料，建立完整的知識背景再出發", "觀察周遭是否有前輩的腳印可以遵循", "想像這個挑戰可能帶來的各種未來結果"], d: ["P", "J", "S", "N"] },
            { q: "處理一件棘手的事物時，你更傾向於？", o: ["對事不對人，追求絕對的公正與邏輯", "對人不對事，優先考慮所有人的感受", "尋求最有效率、耗時最短的捷徑", "尋求最能體現個人價值觀的獨特路徑"], d: ["T", "F", "T", "F"] },
            { q: "你的日常生活步調通常呈現？", o: ["充滿突發驚喜，我隨時準備好調整計畫", "井然有序，如果行程被打亂會感到不安", "追求極致的感官體驗，享受當下的細節", "腦袋總是在想明天或後天，身體活在未來"], d: ["P", "J", "S", "N"] },
            { q: "你認為「讚美」以下哪一點最令你心動？", o: ["你的判斷力非常精準且有邏輯", "你的存在讓身邊的人感到溫暖安心", "你總能看到大家看不見的獨特意義", "你做事非常扎實且讓人感到信任"], d: ["T", "F", "N", "S"] },
            { q: "在派對結束後的深夜，你的感受通常是？", o: ["精力充沛，還想找人繼續聊下去", "徹底斷電，需要至少一天的獨處來充電", "反思剛才聊天中是否有更好的辭令", "感覺剛才的熱鬧很虛幻，懷念安靜"], d: ["E", "I", "F", "I"] },
            { q: "面對一件需要長時間投入的計畫，你會？", o: ["制定詳細的里程碑，按部就班執行", "等待靈感湧現時一口氣爆發完成", "邊做邊修正，保持極大的變動空間", "先想好最壞打算，做好防禦性規劃"], d: ["J", "P", "P", "J"] },
            { q: "你如何定義一個「成功的選擇」？", o: ["它符合數據與客觀利益最大化", "它讓我身邊重要的人都感到快樂", "它讓我能突破現狀，實現自我藍圖", "它是一次安全且經過驗證的正確示範"], d: ["T", "F", "N", "S"] },
            { q: "當你感到壓力時，你的求救方式是？", o: ["找朋友大吐苦水，透過敘述釐清思緒", "把自己關起來，直到理出一個結果", "去購物、大吃或運動，追求體感釋放", "鑽研哲學或理論，試圖看透壓力的本質"], d: ["E", "I", "S", "N"] },
            { q: "你最受不了哪種類型的人？", o: ["邏輯不通且情緒化的人", "冷血、只講規則不講人情的人", "做事拖拉、沒有計畫性的人", "過度死板、扼殺所有創意的人"], d: ["T", "F", "J", "P"] },
            { q: "對於「承諾」，你的看法是？", o: ["一諾千金，絕對要說到做到", "視情況調整，靈活變通才是智慧", "必須白紙黑字，作為未來考核依據", "情感上的契約，重在心意而非形式"], d: ["J", "P", "J", "F"] },
            { q: "你更喜歡哪一種溝通方式？", o: ["開門見山，直接切入核心重點", "溫婉含蓄，先照顧對方的面子與情緒", "天馬行空，不設限地碰撞火花", "詳實紀錄，提供具體的數據與案例"], d: ["T", "F", "N", "S"] },
            { q: "週末下午的獨處，你傾向於？", o: ["整理房間，把積累的雜事清空", "坐在窗邊發呆，任憑思緒飛躍", "沉浸在一部深刻的電影或書籍中", "親自動手做手工藝或烹飪"], d: ["J", "N", "I", "S"] },
            { q: "當你與人發生爭執，你的心態通常是？", o: ["必須釐清到底是誰的邏輯出了錯", "希望儘快和解，哪怕我要先退讓", "覺得這是很好的觀點碰撞機會", "冷漠面對，覺得爭論沒有意義"], d: ["T", "F", "E", "I"] },
            { q: "你的夢想通常是？", o: ["具體的地位、財富或成就里程碑", "一種生活氛圍：自由、平靜且安詳", "改變某個不完美的系統或世界現狀", "守護一份珍貴的感情或傳統文化"], d: ["S", "P", "N", "F"] },
            { q: "對於新科技的態度，你是？", o: ["第一時間入手，享受新功能的創新感", "觀望一陣子，穩定後才會考慮使用", "覺得這些東西只是在簡化人類思考", "必須完全掌握其運作邏輯才願意相信"], d: ["E", "S", "N", "T"] },
            { q: "你如何安排金錢？", o: ["精打細算，每一分錢都有去處", "及時行樂，花錢買體驗最值得", "投資未來，為了長遠目標忍受克制", "隨緣，有錢就花，沒錢就省"], d: ["J", "P", "N", "S"] },
            { q: "你認為「人性」？", o: ["可以透過數據與心理學被預測", "複雜多變，唯有用心感悟", "是一場關於利益分配的博弈", "存在著某種神祕的靈魂連結"], d: ["S", "F", "T", "N"] },
            { q: "工作中遇到錯誤，你的第一動作是？", o: ["修正它，然後分析原因防止再犯", "安慰受影響的人，平復團隊負能量", "檢討流程是否出錯，重新設計架構", "先放著，看看會不會有轉機"], d: ["S", "F", "T", "P"] },
            { q: "你對這份報告的期待是？", o: ["告訴我具體的優缺點與改進方案", "讓我覺得被理解，產生情感共鳴", "開啟我對自我認知的全新窗口", "幫我確認我現在的選擇是否正確"], d: ["T", "F", "N", "S"] }
        ];

        let state = {
            view: 'landing',
            nickname: '',
            zodiac: '',
            currentIdx: 0,
            scores: { E: 0, I: 0, S: 0, N: 0, T: 0, F: 0, J: 0, P: 0 },
            mbtiResult: '',
            feedback: { precision: null, mbtiKnowledge: '', UIExperience: '' }
        };

        const app = document.getElementById('app');

        // --- 核心邏輯 ---

        function render() {
            if (state.view === 'landing') renderLanding();
            else if (state.view === 'quiz') renderQuiz();
            else if (state.view === 'result') renderResult();
            else if (state.view === 'feedback') renderFeedback();
            else if (state.view === 'thanks') renderThanks();
        }

        function renderLanding() {
            app.innerHTML = `
                <div class="space-y-8 py-6 fade-in">
                    <h1 class="text-6xl font-black text-[#7b66ff] tracking-tight">異星座標</h1>
                    <p class="text-[#94a3b8] italic text-xl tracking-widest">靈魂導航實驗室</p>
                    <div class="space-y-4">
                        <input id="nickname" type="text" placeholder="輸入你的暱稱" class="w-full p-5 bg-[#f8faff] rounded-[25px] border border-[#e2e8f0] text-xl text-center outline-none focus:border-[#7b66ff]" value="${state.nickname}">
                        <select id="zodiac" class="w-full p-5 bg-[#f8faff] rounded-[25px] border border-[#e2e8f0] text-xl text-center outline-none focus:border-[#7b66ff] appearance-none cursor-pointer">
                            <option value="">選擇星座標籤</option>
                            ${["牡羊座", "金牛座", "雙子座", "巨蟹座", "獅子座", "處女座", "天秤座", "天蠍座", "射手座", "摩羯座", "水瓶座", "雙魚座"].map(z => `<option value="${z}" ${state.zodiac === z ? 'selected' : ''}>${z}</option>`).join('')}
                        </select>
                    </div>
                    <button onclick="startQuiz()" class="w-full py-6 bg-[#4438ca] text-white text-2xl font-bold rounded-[30px] shadow-lg hover:bg-[#3730a3] transition-all active:scale-95">開啟監測實驗</button>
                </div>
            `;
        }

        function renderQuiz() {
            const q = questions[state.currentIdx];
            const progress = ((state.currentIdx + 1) / questions.length) * 100;
            app.innerHTML = `
                <div class="space-y-6 text-left fade-in">
                    <div class="flex justify-between items-center mb-4">
                        <span class="text-[#7b66ff] font-bold text-lg">數據擷取：${state.currentIdx + 1} / 20</span>
                        <div class="w-24 h-2 bg-[#e2e8f0] rounded-full overflow-hidden">
                            <div class="bg-[#7b66ff] h-full transition-all duration-300" style="width: ${progress}%"></div>
                        </div>
                    </div>
                    <h2 class="text-2xl md:text-3xl font-bold text-[#1e293b] leading-tight mb-8">${q.q}</h2>
                    <div class="space-y-3">
                        ${q.o.map((opt, i) => `
                            <button onclick="handleAnswer('${q.d[i]}')" class="w-full p-5 text-left text-lg bg-[#f8faff] border border-[#e2e8f0] rounded-[20px] hover:border-[#7b66ff] hover:text-[#7b66ff] transition-all">
                                ${opt}
                            </button>
                        `).join('')}
                    </div>
                </div>
            `;
        }

        function renderResult() {
            const advice = getZodiacAdvice(state.mbtiResult, state.zodiac);
            const detail = getDetailAnalysis(state.mbtiResult);
            app.innerHTML = `
                <div class="text-left space-y-8 slide-up">
                    <div class="text-center">
                        <p class="text-lg text-slate-400 mb-1">${state.nickname} 的靈魂座標</p>
                        <h2 class="text-7xl font-black text-[#4438ca] mb-8">${state.mbtiResult}</h2>
                    </div>
                    <div class="space-y-6">
                        <div class="border-l-4 border-[#7b66ff] pl-5">
                            <h3 class="text-[#7b66ff] text-xl font-bold mb-1">💖 情感與友誼</h3>
                            <p class="text-lg text-slate-700">${detail.friend}</p>
                        </div>
                        <div class="border-l-4 border-[#7b66ff] pl-5">
                            <h3 class="text-[#7b66ff] text-xl font-bold mb-1">🧭 愛情模式</h3>
                            <p class="text-lg text-slate-700">${detail.love}</p>
                        </div>
                        <div class="bg-[#f0edff] p-6 rounded-[25px] border-2 border-dashed border-[#7b66ff]">
                            <h3 class="text-[#4438ca] text-xl font-bold mb-2">⭐ 星座標籤性格建議</h3>
                            <p class="text-lg text-[#334155] font-medium italic">對於身為「${state.zodiac}」的你：${advice}</p>
                        </div>
                        <div class="border-l-4 border-slate-300 pl-5">
                            <h3 class="text-slate-500 text-xl font-bold mb-1">👤 生活成長</h3>
                            <p class="text-lg text-slate-700">${detail.life}</p>
                        </div>
                    </div>
                    <button onclick="changeView('feedback')" class="w-full py-5 bg-[#4438ca] text-white text-2xl font-bold rounded-[25px] mt-4 shadow-lg active:scale-95">進入數據回饋</button>
                </div>
            `;
        }

        function renderFeedback() {
            const isPrecisionSelected = state.feedback.precision !== null;
            app.innerHTML = `
                <div class="text-left space-y-8 fade-in">
                    <h2 class="text-3xl font-bold text-center mb-8">精準度校準</h2>
                    <div class="space-y-10">
                        <div>
                            <p class="text-xl font-bold mb-6">1. 您認為分析結果的精準度？</p>
                            <div class="flex justify-between px-2">
                                ${[1, 2, 3, 4, 5].map(num => `
                                    <button onclick="setPrecision(${num})" class="w-14 h-14 rounded-full border-2 flex items-center justify-center font-bold text-xl transition-all ${state.feedback.precision === num ? 'bg-[#7b66ff] text-white border-[#7b66ff] scale-110 shadow-lg' : 'border-[#e2e8f0] text-slate-400 bg-white hover:border-[#7b66ff]'}">
                                        ${num}
                                    </button>
                                `).join('')}
                            </div>
                        </div>
                        <div class="space-y-6">
                            <div>
                                <p class="text-xl font-bold mb-3">2. 您對 MBTI 的了解程度？</p>
                                <select onchange="setFeedbackField('mbtiKnowledge', this.value)" class="w-full p-4 bg-[#f8faff] border rounded-[15px] text-lg outline-none focus:border-[#7b66ff]">
                                    <option value="">請選擇</option>
                                    <option ${state.feedback.mbtiKnowledge === '完全不了解' ? 'selected' : ''}>完全不了解</option>
                                    <option ${state.feedback.mbtiKnowledge === '略有聽聞' ? 'selected' : ''}>略有聽聞</option>
                                    <option ${state.feedback.mbtiKnowledge === '知道自己的型別' ? 'selected' : ''}>知道自己的型別</option>
                                    <option ${state.feedback.mbtiKnowledge === '對理論有深入研究' ? 'selected' : ''}>對理論有深入研究</option>
                                </select>
                            </div>
                            <div>
                                <p class="text-xl font-bold mb-3">3. 本次測驗的整體視覺體驗？</p>
                                <select onchange="setFeedbackField('UIExperience', this.value)" class="w-full p-4 bg-[#f8faff] border rounded-[15px] text-lg outline-none focus:border-[#7b66ff]">
                                    <option value="">請選擇</option>
                                    <option ${state.feedback.UIExperience === '非常精美' ? 'selected' : ''}>非常精美</option>
                                    <option ${state.feedback.UIExperience === '符合期待' ? 'selected' : ''}>符合期待</option>
                                    <option ${state.feedback.UIExperience === '普通' ? 'selected' : ''}>普通</option>
                                    <option ${state.feedback.UIExperience === '需要改進' ? 'selected' : ''}>需要改進</option>
                                </select>
                            </div>
                        </div>
                    </div>
                    <button onclick="changeView('thanks')" class="w-full py-5 text-white text-2xl font-bold rounded-[25px] mt-8 transition-all ${!isPrecisionSelected ? 'bg-slate-300 cursor-not-allowed' : 'bg-[#4438ca] hover:bg-[#3730a3]'}" ${!isPrecisionSelected ? 'disabled' : ''}>
                        完成並儲存數據
                    </button>
                </div>
            `;
        }

        function renderThanks() {
            app.innerHTML = `
                <div class="py-12 space-y-6 fade-in flex flex-col items-center">
                    <svg class="text-[#7b66ff] w-32 h-32" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"></path></svg>
                    <h2 class="text-4xl font-bold text-[#1e293b]">校準完成</h2>
                    <p class="text-xl text-slate-500 leading-relaxed">靈魂數據已成功歸檔。<br>感謝您的貢獻。</p>
                    <button onclick="location.reload()" class="mt-8 text-[#7b66ff] font-bold text-lg hover:underline decoration-2 underline-offset-4">重新進行實驗</button>
                </div>
            `;
        }

        // --- 功能函式 ---

        function startQuiz() {
            const nicknameInput = document.getElementById('nickname');
            const zodiacInput = document.getElementById('zodiac');
            if (!nicknameInput.value || !zodiacInput.value) return;
            state.nickname = nicknameInput.value;
            state.zodiac = zodiacInput.value;
            state.view = 'quiz';
            render();
        }

        function handleAnswer(dim) {
            state.scores[dim]++;
            if (state.currentIdx < questions.length - 1) {
                state.currentIdx++;
                render();
            } else {
                const res = (state.scores.E >= state.scores.I ? 'E' : 'I') +
                            (state.scores.S >= state.scores.N ? 'S' : 'N') +
                            (state.scores.T >= state.scores.F ? 'T' : 'F') +
                            (state.scores.J >= state.scores.P ? 'J' : 'P');
                state.mbtiResult = res;
                state.view = 'result';
                render();
            }
        }

        function setPrecision(val) {
            state.feedback.precision = val;
            renderFeedback();
        }

        function setFeedbackField(field, val) {
            state.feedback[field] = val;
        }

        function changeView(view) {
            state.view = view;
            render();
        }

        function getZodiacAdvice(m, z) {
            const fire = ["牡羊座", "獅子座", "射手座"];
            const water = ["巨蟹座", "天蠍座", "雙魚座"];
            const air = ["雙子座", "天秤座", "水瓶座"];
            const earth = ["金牛座", "處女座", "摩羯座"];
            if (fire.includes(z)) return m.includes('I') ? "作為火象星座卻擁有內向核心的你，經常處於「外冷內熱」的拉扯中。建議在追求個人空間時，也要給予你的熱情一個出口。" : "雙倍的火能量！你的執行力驚人，但要小心過度擴張。建議在行動前先深呼吸三次，避免因衝動忽略細節。";
            if (water.includes(z)) return m.includes('T') ? "你是理性的水，擁有極強洞察力。建議在分析問題之餘，允許自己「感性」一回，直覺與邏輯結合將是無敵武器。" : "溫柔且深邃。你極容易受環境波動影響，建議設定「情緒防線」，保留一塊純淨的領域給自己。";
            if (earth.includes(z)) return m.includes('P') ? "擁有大地的穩重卻渴望靈魂自由。建議在建立穩定物質基礎同時，給予生活 20% 的不確定性。" : "最可靠的堡壘。你對秩序的追求讓你成為定海神針。建議適時放鬆控制欲，接受混亂也是生命美學。";
            if (air.includes(z)) return m.includes('J') ? "靈動的風被賦予了精準航道。建議在嚴格執行計畫時，偶爾脫離軌道飛翔，驚喜往往在空白處產生。" : "無拘無束的自由靈魂。建議在追逐新點子的過程中，練習「收網」藝術，專注完成一件深度的作品。";
            return "";
        }

        function getDetailAnalysis(m) {
            return {
                friend: m.includes('F') ? "你在友情中扮演『療癒者』的角色，對他人的需求極其敏銳。" : "你在友情中扮演『顧問』角色，傾向於提供解決問題的實質方案。",
                love: m.includes('N') ? "你追求靈魂共鳴，容易對『思想有深度』的人產生迷戀，但要小心過度美化對方。" : "你的愛情觀建立在實質陪伴與穩定細節上，『安全感』是你最重要的指標。",
                life: m.includes('J') ? "生活對你而言是一場精準操盤，擅長預見風險，但也難以享受意外驚喜。" : "你活在無限可能中，不願被框架限制，但缺乏節奏感有時會讓你感到生活像長跑。"
            };
        }

        // 初始化
        render();
    </script>
</body>
</html>
