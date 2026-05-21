<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=yes, viewport-fit=cover">
    <title>MTP闯关训练营 | 全面过程控制学习</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;s
        }

        body {
            background-color: #F5F7FA;
            font-family: system-ui, 'Segoe UI', 'Roboto', 'Helvetica Neue', sans-serif;
            padding: 0 0 20px 0;
            color: #1F2937;
        }

        /* 主色调：米其林黄 #FFCC00 / 深蓝 #0033A0 */
        :root {
            --m-blue: #0033A0;
            --m-yellow: #FFCC00;
            --m-yellow-light: #FFF3C4;
            --m-blue-dark: #00257a;
            --gray-bg: #F5F7FA;
            --card-white: #FFFFFF;
            --text-dark: #1F2937;
            --text-muted: #6B7280;
            --success-green: #10B981;
            --border-radius: 20px;
        }

        /* 通用容器 */
        .container {
            max-width: 550px;
            margin: 0 auto;
            padding: 16px 18px;
        }

        /* 头部样式 */
        .header {
            background: var(--m-blue);
            padding: 20px 18px 24px 18px;
            border-radius: 0 0 28px 28px;
            color: white;
            box-shadow: 0 4px 12px rgba(0,0,0,0.08);
        }
        .header h1 {
            font-size: 1.9rem;
            font-weight: 700;
            letter-spacing: -0.3px;
            color: var(--m-yellow);
            margin-bottom: 6px;
        }
        .header p {
            font-size: 0.9rem;
            opacity: 0.9;
        }
        .user-badge {
            background: rgba(255,255,255,0.18);
            border-radius: 40px;
            padding: 6px 14px;
            display: inline-flex;
            align-items: center;
            gap: 8px;
            font-size: 0.8rem;
            margin-top: 12px;
        }

        /* 卡片设计 */
        .card {
            background: var(--card-white);
            border-radius: var(--border-radius);
            padding: 20px 18px;
            margin-top: 20px;
            box-shadow: 0 6px 14px rgba(0,0,0,0.03), 0 2px 4px rgba(0,0,0,0.05);
            border: 1px solid rgba(0,0,0,0.03);
            transition: all 0.2s;
        }

        /* 表单样式 */
        .form-group {
            margin-bottom: 18px;
        }
        label {
            font-weight: 600;
            display: block;
            margin-bottom: 6px;
            color: var(--text-dark);
            font-size: 0.9rem;
        }
        input, select {
            width: 100%;
            padding: 14px 16px;
            border-radius: 28px;
            border: 1.5px solid #E2E8F0;
            font-size: 1rem;
            background: white;
            transition: 0.2s;
        }
        input:focus, select:focus {
            outline: none;
            border-color: var(--m-yellow);
            box-shadow: 0 0 0 3px rgba(255,204,0,0.2);
        }
        .btn {
            display: inline-block;
            background: var(--m-yellow);
            color: var(--m-blue);
            font-weight: 700;
            padding: 14px 20px;
            border: none;
            border-radius: 40px;
            font-size: 1rem;
            width: 100%;
            text-align: center;
            cursor: pointer;
            transition: all 0.2s ease;
            box-shadow: 0 2px 4px rgba(0,0,0,0.05);
        }
        .btn:active {
            transform: scale(0.97);
            background: #e0b400;
        }
        .btn-outline {
            background: transparent;
            border: 2px solid var(--m-yellow);
            color: var(--m-blue);
            box-shadow: none;
        }

        /* 关卡网格 */
        .levels-grid {
            display: flex;
            flex-direction: column;
            gap: 14px;
            margin-top: 12px;
        }
        .level-card {
            background: white;
            border-radius: 24px;
            padding: 16px 18px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            box-shadow: 0 2px 8px rgba(0,0,0,0.04);
            border-left: 6px solid #ccc;
            transition: 0.1s;
            cursor: pointer;
        }
        .level-card.unlocked {
            border-left-color: var(--m-yellow);
            background: white;
        }
        .level-card.locked {
            opacity: 0.7;
            background: #F9FAFB;
            cursor: not-allowed;
            filter: grayscale(0.03);
        }
        .level-info h3 {
            font-size: 1.2rem;
            margin-bottom: 4px;
        }
        .level-info p {
            font-size: 0.75rem;
            color: var(--text-muted);
        }
        .status-badge {
            font-size: 1.5rem;
        }
        .progress-bar {
            background: #E2E8F0;
            border-radius: 30px;
            height: 10px;
            margin: 16px 0 8px;
        }
        .progress-fill {
            background: var(--m-yellow);
            width: 0%;
            height: 10px;
            border-radius: 30px;
        }

        /* 答题页面 */
        .quiz-container {
            margin-top: 10px;
        }
        .question-text {
            font-size: 1.4rem;
            font-weight: 600;
            margin: 12px 0 20px;
            line-height: 1.3;
        }
        .option-item {
            background: #F9FAFB;
            border: 1.5px solid #E5E7EB;
            border-radius: 60px;
            padding: 12px 18px;
            margin-bottom: 12px;
            font-size: 1rem;
            cursor: pointer;
            transition: all 0.1s;
        }
        .option-item.selected {
            background: var(--m-yellow-light);
            border-color: var(--m-yellow);
            font-weight: 500;
        }
        .feedback {
            margin-top: 15px;
            padding: 12px;
            border-radius: 20px;
            background: #F1F5F9;
            font-size: 0.85rem;
        }
        .feedback.correct {
            background: #E6F7EC;
            color: #1E7B4A;
        }
        .feedback.wrong {
            background: #FEF2F2;
            color: #B91C1C;
        }

        /* 勋章和完成页面 */
        .certificate-card {
            text-align: center;
            background: linear-gradient(145deg, #fff 0%, #FFF9E8 100%);
            border: 2px dashed var(--m-yellow);
            padding: 24px;
        }
        .badge-icon {
            font-size: 4rem;
        }
        hr {
            margin: 16px 0;
        }
        .toast-msg {
            position: fixed;
            bottom: 30px;
            left: 50%;
            transform: translateX(-50%);
            background: var(--m-blue);
            color: white;
            padding: 10px 18px;
            border-radius: 40px;
            font-size: 0.85rem;
            z-index: 1000;
            white-space: nowrap;
            box-shadow: 0 4px 12px rgba(0,0,0,0.2);
        }
        .hidden {
            display: none;
        }
        footer {
            text-align: center;
            font-size: 0.7rem;
            color: #9CA3AF;
            margin-top: 28px;
        }
    </style>
</head>
<body>

<!-- 动态视图：使用几个主要面板通过JS切换 -->
<div id="app">
    <!-- 登录页 -->
    <div id="loginView" class="container">
        <div class="header" style="background: var(--m-blue); margin-bottom: 8px;">
            <h1>🏭 MTP闯关营</h1>
            <p>全面过程控制 · 降低波动 · 质量稳定</p>
        </div>
        <div class="card">
            <div class="form-group">
                <label>👤 姓名</label>
                <input type="text" id="inputName" placeholder="例：张伟" autocomplete="off">
            </div>
            <div class="form-group">
                <label>🆔 工号</label>
                <input type="text" id="inputEmpId" placeholder="例：H001234" autocomplete="off">
            </div>
            <div class="form-group">
                <label>🏭 所属BUT</label>
                <select id="inputBut">
                    <option value="CUR BUT">CUR BUT</option>
                    <option value="CAP BUT">CAP BUT</option>
                    <option value="NC BUT">NC BUT</option>
                    <option value="TBM BU1">TBM BU1</option>
                    <option value="其他">其他 (手动填写)</option>
                </select>
                <input type="text" id="otherButInput" placeholder="请填写具体BUT" style="margin-top: 8px; display: none;">
            </div>
            <button id="startBtn" class="btn">🚀 开始闯关之旅</button>
            <div style="font-size: 0.7rem; color: #6B7280; margin-top: 16px; text-align: center;">
                ⚙️ 降低波动 · 从我做起
            </div>
        </div>
    </div>

    <!-- 关卡主页 -->
    <div id="levelsView" class="container hidden">
        <div class="header" style="padding: 16px 18px;">
            <div style="display: flex; justify-content: space-between; align-items: center;">
                <h1 style="font-size: 1.6rem;">📋 MTP关卡</h1>
                <button id="resetProgressBtn" style="background: rgba(255,204,0,0.2); border: none; padding: 6px 12px; border-radius: 30px; color: #FFCC00; font-size: 0.7rem;">重置进度</button>
            </div>
            <div id="userInfoDisplay" class="user-badge">👤 加载中</div>
            <div class="progress-bar"><div id="globalProgressFill" class="progress-fill" style="width:0%"></div></div>
            <div id="progressText" style="font-size:0.75rem; margin-top: 6px;">已通关 0 / 5</div>
        </div>
        <div class="levels-grid" id="levelsGrid"></div>
        <footer>⭐ 每关全部答对即可获得徽章，解锁下一关</footer>
    </div>

    <!-- 答题页面 -->
    <div id="quizView" class="container hidden">
        <div class="header" style="padding: 14px 18px;">
            <button id="backToLevelsBtn" style="background: none; border: none; color: #FFCC00; font-size: 1.2rem; margin-bottom: 8px;">← 返回关卡</button>
            <h2 id="quizLevelTitle" style="font-size: 1.4rem;">关卡 1</h2>
            <div style="font-size:0.8rem;">题目 <span id="qNumber">1</span> / <span id="totalQ">3</span></div>
        </div>
        <div class="card quiz-container">
            <div id="questionArea"></div>
            <div id="optionsArea"></div>
            <button id="submitQuizBtn" class="btn" style="margin-top: 20px;">✓ 提交答案</button>
            <div id="quizFeedback" class="feedback hidden"></div>
        </div>
    </div>

    <!-- 通关完成页面 -->
    <div id="completeView" class="container hidden">
        <div class="header" style="text-align: center;">
            <div style="font-size: 3rem;">🏆🎉</div>
            <h1 style="color: #FFCC00;">毕业啦！</h1>
        </div>
        <div class="card certificate-card">
            <div class="badge-icon">🏅 MTP 见习控制员</div>
            <h3 id="certName">姓名</h3>
            <p id="certEmpId">工号: </p>
            <p id="certBut">BUT: </p>
            <p id="certScore">总得分: 0/15</p>
            <hr>
            <p style="font-size: 0.85rem;">🎯 “降低波动，稳定质量”<br> 感谢你为过程控制贡献力量！</p>
            <button id="saveCertificateBtn" class="btn" style="margin-top: 20px;">📸 保存证书 / 截图</button>
            <button id="restartGameBtn" class="btn-outline btn" style="margin-top: 12px;">🔄 重新学习</button>
        </div>
    </div>
</div>

<script>
    // ---------- 题库 ----------
    const QUIZ_DATA = [
        { // 关卡0
            title: "第1关：波动的“坏脾气”",
            questions: [
                { text: "以下哪种情况属于过程波动？", options: ["A. 设备温度稳定在200±1℃", "B. 挤出速度时快时慢", "C. 同一批次原料规格一致"], correct: 1, explanation: "波动就是过程中的不一致性，速度忽快忽慢会导致质量不稳定，MTP的目标是缩小波动范围。" },
                { text: "过程波动过大会直接导致什么后果？", options: ["A. 设备寿命延长", "B. 产品质量一致性变差", "C. 生产效率必然提高"], correct: 1, explanation: "波动越大，产品质量越不稳定，可能出现超出规格的产品。" },
                { text: "MTP中的‘全面过程控制’首要关注的是？", options: ["A. 最终检查", "B. 过程中的每个环节稳定性", "C. 增加库存"], correct: 1, explanation: "全面过程控制强调从源头到结果的每一步降低波动。" }
            ]
        },
        { // 关卡1
            title: "第2关：MTP的核心做法",
            questions: [
                { text: "降低过程波动最有效的日常动作是？", options: ["A. 凭经验调整参数", "B. 严格遵守标准作业流程SOP", "C. 只关注最终检验结果"], correct: 1, explanation: "严格遵守SOP能减少人为差异，稳定过程输出。" },
                { text: "当发现某一参数超出控制范围时，正确的做法是？", options: ["A. 继续生产不管", "B. 立即停机并上报", "C. 记录下来等下班反馈"], correct: 1, explanation: "及时干预才能防止波动扩大，保证质量稳定。" },
                { text: "SPC（统计过程控制）的主要作用是？", options: ["A. 事后挑选不良品", "B. 实时监控过程波动，提前预警", "C. 增加检验频次"], correct: 1, explanation: "SPC通过控制图及时发现异常波动。" }
            ]
        },
        { // 关卡2
            title: "第3关：过程控制图",
            questions: [
                { text: "控制图中点子超出上下限，表示什么？", options: ["A. 过程正常", "B. 过程出现异常波动", "C. 产品一定不合格"], correct: 1, explanation: "点子出界说明过程存在特殊原因，需调查改善。" },
                { text: "以下哪个工具适合用来查找波动原因？", options: ["A. 鱼骨图", "B. 甘特图", "C. 流程图"], correct: 0, explanation: "鱼骨图（因果图）是分析波动原因的有效工具。" },
                { text: "过程能力指数CpK越高代表？", options: ["A. 过程波动越小越集中", "B. 设备越老旧", "C. 检验越多"], correct: 0, explanation: "CpK越高说明过程稳定且符合规格。" }
            ]
        },
        { // 关卡3
            title: "第4关：一线员工的MTP参与",
            questions: [
                { text: "当你发现某个操作步骤可能导致质量波动时，应该？", options: ["A. 自己改一下继续做", "B. 记录并向BUL反馈建议", "C. 不管它"], correct: 1, explanation: "一线员工是最佳改善者，及时反馈有助于降低波动源。" },
                { text: "标准化作业对MTP的意义是？", options: ["A. 限制员工创造力", "B. 保证作业一致性降低波动", "C. 增加文件工作量"], correct: 1, explanation: "标准化让每个人按最优方法操作，减少变异。" },
                { text: "开展5S活动与过程控制的关系是？", options: ["A. 没有直接关系", "B. 整洁有序的环境减少过程错误波动", "C. 只为了美观"], correct: 1, explanation: "5S能消除寻找浪费、误用等波动来源。" }
            ]
        },
        { // 关卡4
            title: "第5关：MTP带来的好处",
            questions: [
                { text: "全面过程控制最终会带来？", options: ["A. 减少返工和报废", "B. 增加检查次数", "C. 降低生产速度"], correct: 0, explanation: "过程稳定，不良率降低，自然减少返工浪费。" },
                { text: "哪一项是实施MTP的关键收益？", options: ["A. 客户投诉增加", "B. 质量波动减小，交付更可靠", "C. 员工操作更随意"], correct: 1, explanation: "质量稳定赢得客户信任，提升竞争力。" },
                { text: "关于降低波动的说法，正确的是？", options: ["A. 波动无法管理", "B. 系统化管理波动可以持续改进质量", "C. 只有质检员需要负责"], correct: 1, explanation: "波动可测量、可降低，全员参与过程控制。" }
            ]
        }
    ];

    const TOTAL_LEVELS = QUIZ_DATA.length; // 5关

    // 全局存储
    let currentUser = null;     // { name, empId, but }
    let levelStatus = [];       // 每关是否完成（解锁条件：前一个完成或关卡0完成）
    let levelScores = [];       // 存储每关答对了几题（通关需要等于3）
    let currentQuizLevel = 0;   // 当前答题是第几关(索引)
    let currentQuestionIdx = 0;
    let selectedAnswers = [];    // 当前关卡用户选择的临时答案（索引存储选项下标）
    let userAnswersRecord = [];   // 用于存储当前关卡已经正确提交的题目，避免重复提交后跳题逻辑，但其实我们通过逐个正确才能下一题模式: 每次提交只处理当前题目，正确则下一题
    // 为了实现类似“必须答对当前题才能前进”, 我们在每道题提交校验，正确就+1，错误给提示
    let currentQuizAnswers = [];   // 存储当前题目用户临时选择的选项索引（未提交时）
    let quizCompletedCorrectCount = 0; // 当前关卡已正确答对的数量

    // 辅助函数
    function saveToLocal() {
        if (!currentUser) return;
        const data = {
            user: currentUser,
            levelStatus: levelStatus,
            levelScores: levelScores,
        };
        localStorage.setItem(`MTP_${currentUser.empId}`, JSON.stringify(data));
    }

    function loadFromLocal(empId) {
        const raw = localStorage.getItem(`MTP_${empId}`);
        if (!raw) return null;
        try {
            return JSON.parse(raw);
        } catch(e) { return null; }
    }

    function initNewProgress() {
        levelStatus = new Array(TOTAL_LEVELS).fill(false);
        levelScores = new Array(TOTAL_LEVELS).fill(0);
        if (TOTAL_LEVELS > 0) levelStatus[0] = true; // 第一关初始解锁
    }

    // 刷新关卡页面UI
    function renderLevels() {
        const grid = document.getElementById('levelsGrid');
        if (!grid) return;
        let completedCount = levelStatus.filter(v => v === true && levelScores[levelStatus.indexOf(v)] === 3).length;
        // 但关卡完成判断: 分数等于3
        let trulyCompleted = 0;
        for(let i=0;i<TOTAL_LEVELS;i++) {
            if(levelScores[i] === 3) trulyCompleted++;
        }
        const totalCompleted = trulyCompleted;
        document.getElementById('progressText').innerHTML = `已通关 ${totalCompleted} / ${TOTAL_LEVELS}`;
        const percent = (totalCompleted / TOTAL_LEVELS) * 100;
        document.getElementById('globalProgressFill').style.width = `${percent}%`;
        
        let html = '';
        for(let i=0;i<TOTAL_LEVELS;i++) {
            const isUnlocked = levelStatus[i];
            const isCompleted = (levelScores[i] === 3);
            let statusIcon = '';
            if(isCompleted) statusIcon = '✅';
            else if(isUnlocked) statusIcon = '🔓';
            else statusIcon = '🔒';
            const borderClass = isUnlocked ? 'unlocked' : 'locked';
            html += `
                <div class="level-card ${borderClass}" data-level="${i}">
                    <div class="level-info">
                        <h3>📘 ${QUIZ_DATA[i].title} ${isCompleted ? '(通关)' : ''}</h3>
                        <p>${isCompleted ? '已完成，满分通过' : (isUnlocked ? '点击开始闯关' : '请先通过前一关')}</p>
                    </div>
                    <div class="status-badge">${statusIcon}</div>
                </div>
            `;
        }
        grid.innerHTML = html;
        // 绑定点击事件
        document.querySelectorAll('.level-card').forEach(card => {
            card.addEventListener('click', (e) => {
                const lvl = parseInt(card.dataset.level);
                if(levelStatus[lvl]) {
                    startQuiz(lvl);
                } else {
                    showToast('🔒 需要先完成前一关才能解锁！');
                }
            });
        });
    }

    function startQuiz(levelIdx) {
        currentQuizLevel = levelIdx;
        currentQuestionIdx = 0;
        quizCompletedCorrectCount = 0;
        selectedAnswers = [];
        // 重置当前关卡已正确数（因为可能重新进入）
        // 但注意: 如果这关已经通关，不应该进入答题, 应阻止
        if(levelScores[levelIdx] === 3) {
            showToast('🏆 你已经通关本关卡！');
            return;
        }
        // 加载题目
        loadQuestionForCurrent();
        showView('quizView');
        document.getElementById('quizLevelTitle').innerText = QUIZ_DATA[levelIdx].title;
        document.getElementById('totalQ').innerText = QUIZ_DATA[levelIdx].questions.length;
        document.getElementById('quizFeedback').classList.add('hidden');
    }

    function loadQuestionForCurrent() {
        const levelData = QUIZ_DATA[currentQuizLevel];
        const q = levelData.questions[currentQuestionIdx];
        document.getElementById('qNumber').innerText = currentQuestionIdx+1;
        const questionHtml = `<div class="question-text">${q.text}</div>`;
        document.getElementById('questionArea').innerHTML = questionHtml;
        let optsHtml = '';
        q.options.forEach((opt, idx) => {
            optsHtml += `<div class="option-item" data-opt-index="${idx}">${opt}</div>`;
        });
        document.getElementById('optionsArea').innerHTML = optsHtml;
        // 绑定选项点击样式
        document.querySelectorAll('.option-item').forEach(optDiv => {
            optDiv.addEventListener('click', (e) => {
                document.querySelectorAll('.option-item').forEach(el => el.classList.remove('selected'));
                optDiv.classList.add('selected');
                currentQuizAnswers = [parseInt(optDiv.dataset.optIndex)];
            });
        });
        document.getElementById('quizFeedback').classList.add('hidden');
        currentQuizAnswers = [];
    }

    function submitCurrentQuestion() {
        if(!currentQuizAnswers.length) {
            showToast('请先选择一个答案');
            return;
        }
        const levelData = QUIZ_DATA[currentQuizLevel];
        const currentQ = levelData.questions[currentQuestionIdx];
        const isCorrect = (currentQuizAnswers[0] === currentQ.correct);
        const feedbackDiv = document.getElementById('quizFeedback');
        feedbackDiv.classList.remove('hidden', 'correct', 'wrong');
        if(isCorrect) {
            feedbackDiv.innerHTML = `✅ 答对了！ ${currentQ.explanation || ''}`;
            feedbackDiv.classList.add('correct');
            // 正确，增加计数，移动到下一题
            quizCompletedCorrectCount++;
            if(quizCompletedCorrectCount === levelData.questions.length) {
                // 通关完成
                levelScores[currentQuizLevel] = 3;
                // 解锁下一关
                if(currentQuizLevel + 1 < TOTAL_LEVELS) {
                    levelStatus[currentQuizLevel+1] = true;
                }
                saveToLocal();
                showToast(`🎉 恭喜通过${QUIZ_DATA[currentQuizLevel].title}！获得勋章`);
                renderLevels();
                showView('levelsView');
                return;
            } else {
                // 移到下一题
                currentQuestionIdx++;
                loadQuestionForCurrent();
            }
        } else {
            feedbackDiv.innerHTML = `❌ 答错了！ ${currentQ.explanation || '再试试看，理解波动控制精髓。'}`;
            feedbackDiv.classList.add('wrong');
            // 允许重试，不清空选项，保留选择需要重新选
        }
    }

    // 视图切换
    function showView(viewId) {
        document.getElementById('loginView').classList.add('hidden');
        document.getElementById('levelsView').classList.add('hidden');
        document.getElementById('quizView').classList.add('hidden');
        document.getElementById('completeView').classList.add('hidden');
        document.getElementById(viewId).classList.remove('hidden');
    }

    function showToast(msg) {
        let toast = document.querySelector('.toast-msg');
        if(toast) toast.remove();
        let div = document.createElement('div');
        div.className = 'toast-msg';
        div.innerText = msg;
        document.body.appendChild(div);
        setTimeout(() => div.remove(), 2000);
    }

    // 开始或续玩
    function startOrResume(user) {
        currentUser = user;
        const saved = loadFromLocal(user.empId);
        if(saved && saved.levelStatus) {
            levelStatus = saved.levelStatus;
            levelScores = saved.levelScores;
        } else {
            initNewProgress();
        }
        // 展示关卡页
        document.getElementById('userInfoDisplay').innerHTML = `👤 ${user.name} | 🆔 ${user.empId} | 🏭 ${user.but}`;
        renderLevels();
        showView('levelsView');
        saveToLocal();
    }

    // 重置进度
    function resetProgress() {
        if(confirm('⚠️ 重置会清空所有闯关记录，确定吗？')) {
            initNewProgress();
            saveToLocal();
            renderLevels();
            showToast('进度已重置，从第一关开始');
        }
    }

    // 完整通关查看毕业证
    function checkAllCompleteAndShowCert() {
        let allComplete = true;
        for(let i=0;i<TOTAL_LEVELS;i++) {
            if(levelScores[i] !== 3) { allComplete = false; break; }
        }
        if(allComplete && currentUser) {
            // 总得分
            let totalCorrect = levelScores.reduce((a,b)=>a+b,0);
            document.getElementById('certName').innerHTML = `🏅 ${currentUser.name}`;
            document.getElementById('certEmpId').innerHTML = `工号: ${currentUser.empId}`;
            document.getElementById('certBut').innerHTML = `BUT: ${currentUser.but}`;
            document.getElementById('certScore').innerHTML = `总得分: ${totalCorrect}/${TOTAL_LEVELS*3}`;
            showView('completeView');
        } else {
            showToast('需要完成全部5个关卡才能获得证书，继续加油！');
        }
    }

    // 事件绑定
    document.getElementById('startBtn').addEventListener('click', () => {
        const name = document.getElementById('inputName').value.trim();
        const empId = document.getElementById('inputEmpId').value.trim();
        let butVal = document.getElementById('inputBut').value;
        if(butVal === '其他') {
            butVal = document.getElementById('otherButInput').value.trim();
            if(!butVal) { showToast('请输入具体BUT'); return; }
        }
        if(!name || !empId) { showToast('请填写姓名和工号'); return; }
        startOrResume({ name, empId, but: butVal });
    });
    document.getElementById('resetProgressBtn')?.addEventListener('click', resetProgress);
    document.getElementById('backToLevelsBtn')?.addEventListener('click', () => showView('levelsView'));
    document.getElementById('submitQuizBtn')?.addEventListener('click', submitCurrentQuestion);
    document.getElementById('saveCertificateBtn')?.addEventListener('click', () => {
        alert('📸 请使用手机截图保存证书，恭喜毕业！');
    });
    document.getElementById('restartGameBtn')?.addEventListener('click', () => {
        resetProgress();
        showView('levelsView');
    });
    // 监听BUT切换显示自定义框
    document.getElementById('inputBut').addEventListener('change', (e) => {
        const otherInput = document.getElementById('otherButInput');
        if(e.target.value === '其他') otherInput.style.display = 'block';
        else otherInput.style.display = 'none';
    });
    // 在关卡页面增加证书入口
    const headerDiv = document.querySelector('#levelsView .header');
    const certBtn = document.createElement('button');
    certBtn.innerText = '🏅 毕业证书';
    certBtn.style.cssText = 'background:#FFCC00; border:none; border-radius:20px; padding:6px 14px; margin-left: 8px; color:#0033A0; font-weight:bold;';
    certBtn.addEventListener('click', () => checkAllCompleteAndShowCert());
    if(headerDiv) headerDiv.querySelector('div').appendChild(certBtn);
</script>
</body>
</html>
```
