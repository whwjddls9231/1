<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>옛날과 오늘날의 풍습 비교 학습</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        /* Custom Font */
        @import url('https://fonts.googleapis.com/css2?family=Dokdo&family=Noto+Serif+KR:wght@200..900&display=swap');
        
        /* 제목 외 모든 글의 폰트를 Noto Serif KR로 변경 */
        :root { font-family: 'Noto Serif KR', serif; }
        
        /* 제목 폰트는 Dokdo를 유지 */
        .jua-font { font-family: 'Dokdo', cursive; } 
        
        /* 새로운 전통적인 색상 정의 */
        .bg-hanji { 
            background-color: #f8f5e9; /* 한지 느낌의 밝은 배경 */
            /* 전통 문양 느낌의 아주 연한 SVG 패턴 추가 */
            background-image: url("data:image/svg+xml,%3Csvg width='40' height='40' viewBox='0 0 40 40' xmlns='http://www.w3.org/2000/svg'%3E%3Cg fill='%23e0d8c0' fill-opacity='0.4'%3E%3Cpath d='M40 0H20L0 20V40h20l20-20zM0 0h20L40 20V0z'/%3E%3C/g%3E%3C/svg%3E");
            background-size: 40px 40px; 
        } 
        .text-dark-accent { color: #695241; } /* 진한 갈색/프레임 색상 */
        .bg-dark-accent { background-color: #695241; }
        .text-past-accent { color: #f08080; } /* 과거 강조색 (산호색) */
        .bg-past-accent-light { background-color: #fcebeb; } /* 과거 배경 (매우 연한 산호색) */
        .text-present-accent { color: #72c262; } /* 오늘날 강조색 (녹색) */
        .bg-present-accent-light { background-color: #ebfceb; } /* 오늘날 배경 (매우 연한 녹색) */

        /* Custom CSS for Fill-in-the-Blank Input Styling */
        .blank-input {
            width: 80px;
            min-width: 50px;
            max-width: 150px;
            text-align: center;
            border: 2px solid #9ca3af; 
            border-radius: 6px;
            padding: 2px 4px;
            margin: 0 4px;
            display: inline-block;
            transition: all 0.3s ease-in-out;
            background-color: #f9fafb; 
            color: #1e293b; 
        }
        .blank-input.correct {
            border-color: #10b981 !important; 
            background-color: #ecfdf5 !important; 
        }
        .blank-input.incorrect {
            border-color: #ef4444 !important; 
            background-color: #fef2f2 !important; 
        }
        
        /* Answer display logic (Not used anymore but keeping structure) */
        .blank-answer {
            color: #1d4ed8; 
            font-weight: 700;
            display: none;
        }

        /* Card Flip Styles */
        .flip-card-container {
            perspective: 1000px;
        }
        .flip-card-inner {
            transition: transform 0.8s;
            transform-style: preserve-3d;
            height: 100%;
            position: relative;
        }
        .flip-card-inner.flipped {
            transform: rotateY(180deg);
        }
        .card-face {
            position: absolute;
            width: 100%;
            height: 100%;
            backface-visibility: hidden;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            padding: 1.5rem;
            border-radius: 0.75rem;
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
            min-height: 250px; 
            background-color: #ffffff; /* 카드 배경은 흰색 유지 */
        }
        .card-front {
            border-top: 4px solid #f08080; /* 과거 Accent (산호색) */
        }
        .card-back {
            border-top: 4px solid #72c262; /* 오늘날 Accent (녹색) */
            transform: rotateY(180deg);
        }

        /* --- Dramatic Page Transition Styles --- */
        .page-transition {
            transition: opacity 1.2s ease-in-out, transform 1.2s ease-in-out;
        }
        
        /* Style for the screen to dramatically exit */
        .page-exit {
            opacity: 0 !important;
            transform: scale(0.5) rotateX(15deg) !important;
        }
        
        /* Style for the new quiz screen to dramatically enter */
        .page-enter {
            opacity: 0;
            transform: scale(1.3);
        }
        .page-enter.ready {
            opacity: 1;
            transform: scale(1);
            transition: opacity 1s ease-out, transform 1s ease-out;
        }
        
        /* Custom radio button style for Quiz (IMPROVED for selection visibility) */
        .quiz-option {
            background-color: #ffffff;
            border: 2px solid #e5e7eb;
            transition: all 0.2s;
            color: #1e293b; /* Default text color */
        }
        .quiz-option:hover {
            background-color: #f3f4f6;
            border-color: #695241;
        }
        
        /* State when the radio button is CHECKED */
        .quiz-option input[type="radio"]:checked + span {
            background-color: #f7a94a; /* Selecting color: Orange */
            color: white;
            border-color: #f7a94a;
            box-shadow: 0 4px 6px -1px rgba(247, 169, 74, 0.5), 0 2px 4px -2px rgba(247, 169, 74, 0.5);
            transform: scale(1.02);
        }
        
        /* State when the answer is CORRECT (Green) */
        .quiz-option.correct {
            background-color: #10b981; 
            color: white;
            border-color: #10b981;
            transform: scale(1.02);
        }
        
        /* State when the answer is INCORRECT (Red) */
        .quiz-option.incorrect {
            background-color: #ef4444; 
            color: white;
            border-color: #ef4444;
        }
        
        /* Quiz title animation */
        @keyframes bounce {
            0%, 100% { transform: translateY(-5%); }
            50% { transform: translateY(0); }
        }
        .animate-bounce-stage {
            animation: bounce 1s infinite;
        }
    </style>
</head>
<!-- Initial Body styling for smooth transition -->
<body class="bg-hanji min-h-screen p-4 md:p-8 page-transition">

    <!-- Header - Updated for traditional colors -->
    <header class="text-center mb-8">
        <h1 class="text-5xl font-bold mb-4 jua-font text-dark-accent">
            ⭐ 옛날과 오늘날의 풍습 비교 학습 ⭐
        </h1>
        <p class="text-xl text-white bg-dark-accent inline-block py-2 px-4 rounded-full font-extrabold shadow-lg transition duration-300 transform hover:scale-105">
            카드를 눌러 풍습의 변화를 확인하고, 빈칸을 채워보세요! 👀
        </p>
    </header>
    
    <!-- Progress Bar Section (Sticky) -->
    <div id="progress-container" class="sticky top-0 z-10 bg-hanji/95 p-3 rounded-lg shadow-xl border-b-4 border-dark-accent mb-6 backdrop-blur-sm">
        <h2 class="text-lg font-bold text-dark-accent mb-1">진행도: <span id="progress-text">0/28 (0%)</span></h2>
        <div class="w-full h-4 bg-gray-300 rounded-full overflow-hidden">
            <div id="progress-bar" class="h-full bg-red-400 rounded-full transition-all duration-500 ease-out shadow-inner" style="width: 0%;"></div>
        </div>
    </div>

    <main id="app-container" class="max-w-4xl mx-auto space-y-8">
        <!-- Topic Cards and Static Sections will be rendered here by JavaScript -->
    </main>
    
    <!-- NEW: Master Quiz Force Start Button -->
    <div class="max-w-4xl mx-auto p-4 text-center mt-6">
        <button id="force-start-button" onclick="checkCompletionAndStartQuiz(true)" 
                class="bg-blue-600 hover:bg-blue-700 text-white font-bold py-3 px-6 rounded-full shadow-xl transition duration-300 transform hover:scale-105">
            🚀 마스터 퀴즈 바로 시작하기 (테스트용)
        </button>
    </div>

    <!-- Modal for messages -->
    <div id="message-modal" class="fixed inset-0 bg-gray-600 bg-opacity-50 hidden items-center justify-center p-4 z-50">
        <div class="bg-white rounded-xl shadow-2xl p-6 max-w-sm w-full">
            <h3 id="modal-title" class="text-xl font-semibold mb-3 text-dark-accent">알림</h3>
            <p id="modal-text" class="text-gray-700 mb-4">메시지 내용</p>
            <button onclick="closeModal()" class="w-full bg-dark-accent hover:bg-[#523f33] text-white font-bold py-2 px-4 rounded-lg transition duration-200">확인</button>
        </div>
    </div>

    <script>
        // Original Data Structure
        const allQuestions = [
            { id: 1, section: '1. 일상생활 속 풍습의 변화', title: '1-1. 돌잔치', type: '과거', 
              text: '옛날에는 아기가 태어난 지 [1]이 되면 아이의 건강을 축하하는 의미로 [2]를 하였습니다.', 
              answers: ['1년', '돌잔치'] },
            { id: 2, section: '1. 일상생활 속 풍습의 변화', title: '1-1. 돌잔치', type: '오늘날', 
              text: '오늘날에는 돌잔치를 [3] 하거나 간소하게 진행하기도 합니다. 직업의 다양화로 [4]에 사용되는 물건도 새로 생겨났습니다.', 
              answers: ['안', '돌잡이'] },
            { id: 3, section: '1. 일상생활 속 풍습의 변화', title: '1-2. 결혼식', type: '과거', 
              text: '[5]에서 정해 준 상대와 결혼하였으며, [6] 집에서 [7] [8]을 입고 결혼식을 올린 뒤, 나중에 [9] 집으로 가서 살았습니다.', 
              answers: ['집안', '신부', '전통', '한복', '신랑'] },
            { id: 4, section: '1. 일상생활 속 풍습의 변화', title: '1-2. 결혼식', type: '오늘날', 
              text: '결혼식 형식이 [10]해졌으며, 결혼식 과정도 개인의 [11]에 따라 달라졌습니다.', 
              answers: ['다양', '선택'] },
            { id: 5, section: '1. 일상생활 속 풍습의 변화', title: '1-3. 장례식', type: '과거', 
              text: '돌아가신 분을 땅에 묻고 [12]일이나 [13]일 동안 장례를 치렀습니다. 이후 시기와 때를 맞춰 [14]하고 [15]를 지냈습니다.', 
              answers: ['5', '7', '성묘', '제사'] },
            { id: 6, section: '1. 일상생활 속 풍습의 변화', title: '1-3. 장례식', type: '오늘날', 
              text: '오늘날에는 주로 [16]일 동안 장례를 치릅니다. 돌아가신 분은 [17]하여 [18]에 모시는 경우가 점점 많아지고, [19]을 간단하게 차리기도 합니다.', 
              answers: ['3', '화장', '납골당', '제사상'] },
            { id: 7, section: '1. 일상생활 속 풍습의 변화', title: '1-4. 놀이', type: '과거', 
              text: '[20]에서 사람들과 함께하는 놀이가 많았습니다.', 
              answers: ['자연'] },
            { id: 8, section: '1. 일상생활 속 풍습의 변화', title: '1-4. 놀이', type: '오늘날', 
              text: '[21]이나 [22]를 이용해 친구들과 게임을 즐깁니다.', 
              answers: ['스마트폰', '컴퓨터'] },
            { id: 9, section: '2. 세시 풍속의 변화', title: '세시 풍속의 의미', type: '과거', 
              text: '옛날 사람들은 주로 농사를 지으며 살았습니다. 그래서 [23]가 잘되고 사람들이 [24]하게 살기를 바라는 마음을 담아 계절이나 명절에 따라 다양한 풍습을 지켰습니다.', 
              answers: ['농사', '건강'] },
            { id: 10, section: '2. 세시 풍속의 변화', title: '2. 세시 풍속의 변화', type: '오늘날', 
              text: '오늘날의 풍습은 옛날과 달라졌지만, 가족이 함께 모여 음식을 만들고 서로의 [25]과 [26]을 바라는 마음은 오늘날에도 계속되고 있습니다.', 
              answers: ['건강', '행복'] },
            { id: 11, section: '변화 정리', title: '핵심 정리', type: '요약', 
              text: '→ 오늘날에는 각자의 선택에 따라 풍습이 [27]해졌으며, 옛날보다 과정이나 형식이 [28]해졌습니다.', 
              answers: ['다양', '간단'] }
        ];

        // Group data into flippable topics
        const topicGroups = [
            { title: '돌잔치', idPrefix: 'doljanchi', past: allQuestions.find(q => q.id === 1), present: allQuestions.find(q => q.id === 2), emoji: '👶🎂' },
            { title: '결혼식', idPrefix: 'wedding', past: allQuestions.find(q => q.id === 3), present: allQuestions.find(q => q.id === 4), emoji: '💍🎎' },
            { title: '장례식', idPrefix: 'funeral', past: allQuestions.find(q => q.id === 5), present: allQuestions.find(q => q.id === 6), emoji: '🕯️🙏' },
            { title: '놀이', idPrefix: 'play', past: allQuestions.find(q => q.id === 7), present: allQuestions.find(q => q.id === 8), emoji: '🎮⚽' },
        ];

        // Static content sections
        const staticSections = [
            { data: allQuestions.find(q => q.id === 9), emoji: '🌾🗓️' }, // 세시 풍속
            { data: allQuestions.find(q => q.id === 10), emoji: '👨‍👩‍👧‍👦💖' }, // 세시 풍속 변화
            { data: allQuestions.find(q => q.id === 11), emoji: '💡✨' }, // 핵심 정리
        ];

        // --- NEW GLOBAL STATE & CONSTANTS FOR QUIZ ---
        const TOTAL_BLANKS = allQuestions.reduce((sum, q) => sum + q.answers.length, 0); // Total 28 blanks
        let isMasterQuizActive = false;
        let masterQuizStage = 0;

        // NEW: 객관식/OX로 구성된 최종 퀴즈 문제 목록
        const finalQuizQuestions = [
            { 
                type: 'OX', 
                q: "옛날에는 아기가 태어난 지 1년이 되는 날, 돌잔치를 열어 건강을 축하했습니다. (O/X)", 
                options: ["O", "X"],
                a: "O" 
            },
            { 
                type: 'MCQ', 
                q: "옛날 결혼식에서, 결혼식을 올린 뒤 신랑 집으로 가서 살았던 사람은?", 
                options: ["신랑", "신부", "중매쟁이", "주례사"], 
                a: "신부" 
            },
            { 
                type: 'MCQ', 
                q: "오늘날 장례 풍습에 대한 설명으로 옳은 것은?", 
                options: [
                    "① 돌아가신 분을 땅에 묻는 매장 방식이 대부분이다.",
                    "② 장례 기간은 보통 옛날과 같이 5일이나 7일 동안 치러진다.",
                    "③ 돌아가신 분을 화장하여 납골당에 모시는 경우가 많다.",
                    "④ 제사는 반드시 옛 방식대로 복잡하게 차려야 한다."
                ], 
                a: "③ 돌아가신 분을 화장하여 납골당에 모시는 경우가 많다."
            },
            { 
                type: 'OX', 
                q: "오늘날의 놀이 풍습은 옛날처럼 자연에서 사람들과 함께하는 놀이가 주를 이룹니다. (O/X)", 
                options: ["O", "X"],
                a: "X" 
            },
            { 
                type: 'MCQ', 
                q: "오늘날 풍습 변화의 핵심 특징으로 가장 알맞은 것은?", 
                options: [
                    "① 모두 전통 한복을 입고 행사를 진행해야 한다.",
                    "② 과정이나 형식이 옛날보다 훨씬 복잡해졌다.",
                    "③ 각자의 선택에 따라 다양해졌으며, 과정이 간단해졌다.",
                    "④ 오직 가족 단위로만 행사를 치러야 한다."
                ], 
                a: "③ 각자의 선택에 따라 다양해졌으며, 과정이 간단해졌다."
            }
        ];


        // Utility to show custom modal instead of alert()
        function showModal(title, text) {
            const modal = document.getElementById('message-modal');
            document.getElementById('modal-title').textContent = title;
            document.getElementById('modal-text').textContent = text;
            modal.classList.remove('hidden');
            modal.classList.add('flex');
        }

        function closeModal() {
            const modal = document.getElementById('message-modal');
            modal.classList.add('hidden');
            modal.classList.remove('flex');
        }

        // Function to dynamically adjust input width based on content
        function adjustInputWidth(input) {
            const textWidth = input.value.length * 15 + 20; 
            input.style.width = Math.min(Math.max(textWidth, 60), 200) + 'px';
        }

        // Function to handle card click (flip)
        function flipCard(cardInnerElement) {
            if (isMasterQuizActive) return; // Cannot flip if master quiz is active
            cardInnerElement.classList.toggle('flipped');
        }
        
        // --- NEW FUNCTIONS FOR PROGRESS AND COMPLETION ---

        function updateProgress(correctCount) {
            const percentage = Math.round((correctCount / TOTAL_BLANKS) * 100);
            const progressBar = document.getElementById('progress-bar');
            const progressText = document.getElementById('progress-text');
            const forceStartButton = document.getElementById('force-start-button');

            if (progressBar && progressText) {
                progressBar.style.width = `${percentage}%`;
                progressText.textContent = `${correctCount}/${TOTAL_BLANKS} (${percentage}%)`;
                
                // Progress color change effect
                if (percentage < 33) {
                    progressBar.className = 'h-full rounded-full transition-all duration-500 ease-out shadow-inner bg-red-400';
                } else if (percentage < 66) {
                    progressBar.className = 'h-full rounded-full transition-all duration-500 ease-out shadow-inner bg-yellow-400';
                } else if (percentage < 100) {
                    progressBar.className = 'h-full rounded-full transition-all duration-500 ease-out shadow-inner bg-blue-400';
                } else {
                    // 100% completion color
                    progressBar.className = 'h-full rounded-full transition-all duration-500 ease-out bg-green-500 shadow-xl shadow-green-300';
                }
            }

            // Hide the force start button if 100% completed naturally
            if (percentage === 100 && forceStartButton) {
                 forceStartButton.style.display = 'none';
            }
        }

        function instantCheck(input) {
            if (isMasterQuizActive) return;

            const correctAnswer = input.dataset.correctAnswer;
            const userAnswer = input.value.trim();
            
            input.classList.remove('correct', 'incorrect');
            input.style.borderColor = '#9ca3af'; // Reset border color for instant feedback

            if (userAnswer === '') {
                // Do not mark as incorrect if empty, just reset style
            } else {
                // Case-insensitive comparison
                if (userAnswer.toLowerCase() === correctAnswer.toLowerCase()) {
                    input.classList.add('correct');
                } else {
                    input.classList.add('incorrect');
                }
            }
            
            // Recalculate Total Correct and Check Completion
            const allInputs = document.querySelectorAll('.blank-input');
            let currentCorrect = 0;
            
            allInputs.forEach(i => {
                if (i.classList.contains('correct')) {
                    currentCorrect++;
                }
            });
            
            updateProgress(currentCorrect);
            
            if (currentCorrect === TOTAL_BLANKS) {
                // Small delay to let the final correct color show up
                setTimeout(() => checkCompletionAndStartQuiz(false), 500);
            }
        }

        /**
         * Checks completion and starts the quiz.
         * @param {boolean} force - If true, starts the quiz regardless of completion status.
         */
        function checkCompletionAndStartQuiz(force) {
            if (isMasterQuizActive) return;

            if (!force) {
                // Check if all blanks are filled correctly (Only proceed if not forced)
                const allInputs = document.querySelectorAll('.blank-input');
                let currentCorrect = 0;
                allInputs.forEach(i => {
                    if (i.classList.contains('correct')) {
                        currentCorrect++;
                    }
                });
                if (currentCorrect !== TOTAL_BLANKS) {
                    showModal("⚠️ 아직 학습 중", "모든 빈칸을 정확하게 채워야 마스터 퀴즈가 시작됩니다! 빈칸을 마저 채워주세요. (강제 시작 버튼을 누르셨다면, 테스트가 바로 시작됩니다.)");
                    return;
                }
                showModal("✅ 100% 달성!", "축하합니다! 모든 빈칸을 채우셨습니다. 이제 '풍습 마스터' 퀴즈에 도전하세요!");
            } else {
                showModal("🚀 마스터 퀴즈 시작!", "테스트 버튼으로 최종 퀴즈를 시작합니다!");
            }

            isMasterQuizActive = true;
            
            // 1. Dramatic screen transition: Apply exit style to the current body
            document.body.classList.add('page-exit');

            // 2. Wait for the exit animation to complete (1200ms)
            setTimeout(() => {
                
                // 3. Reset body style and replace content with the quiz HTML
                document.body.classList.remove('page-exit');
                document.body.classList.add('page-transition'); 
                document.body.innerHTML = renderFinalQuiz();
                
                // 4. Trigger the entrance animation
                const quizContainer = document.querySelector('.quiz-wrapper');
                requestAnimationFrame(() => {
                    requestAnimationFrame(() => {
                        if (quizContainer) {
                            quizContainer.classList.add('ready');
                        }
                    });
                });
                
            }, 1200); 
        }
        
        function renderFinalQuiz() {
            const currentQ = finalQuizQuestions[masterQuizStage];
            
            let optionsHtml = '';
            
            // Generate HTML for options (MCQ or OX)
            optionsHtml = currentQ.options.map((option, index) => {
                // Use a generic index 'i' for mapping for clean HTML
                const inputId = `quiz-opt-${masterQuizStage}-${index}`; 
                return `
                    <label for="${inputId}" class="flex items-center space-x-3 mb-3 cursor-pointer">
                        <!-- Use radio button's checked state to style the sibling span -->
                        <input type="radio" id="${inputId}" name="quiz-answer" value="${option.trim()}" class="hidden" 
                            onchange="handleSelection(this)" />
                        <span class="quiz-option flex-1 block p-3 rounded-xl text-lg font-medium text-gray-700 hover:text-dark-accent 
                            ${currentQ.type === 'OX' ? 'text-3xl font-extrabold' : ''}">
                            ${option}
                        </span>
                    </label>
                `;
            }).join('');
            
            // Clear any old selection highlight classes on the options container
            document.querySelectorAll('.quiz-option').forEach(el => el.classList.remove('correct', 'incorrect'));


            // Wrap the entire new page content in a div with transition classes
            let html = `
                <div class="quiz-wrapper page-transition page-enter bg-hanji min-h-screen p-4 md:p-8">
                    <header class="text-center mb-12 p-8 pt-12">
                        <h1 class="text-5xl md:text-6xl font-extrabold jua-font text-red-600 mb-4 animate-bounce-stage">
                            Stage ${masterQuizStage + 1} / ${finalQuizQuestions.length}
                        </h1>
                        <p class="text-2xl text-dark-accent font-semibold">✨ 풍습 마스터 퀴즈 도전! ✨</p>
                    </header>
                    <main class="max-w-xl mx-auto p-8 rounded-2xl shadow-2xl bg-white border-8 border-yellow-500">
                        <div id="quiz-content">
                            <p class="text-2xl font-bold text-gray-700 mb-6">${currentQ.q}</p>
                            
                            <div id="quiz-options" class="space-y-4">
                                ${optionsHtml}
                            </div>
                            
                            <button id="submit-button" onclick="checkFinalAnswer()" class="w-full mt-8 bg-blue-500 hover:bg-blue-600 text-white text-xl font-bold py-3 rounded-xl transition shadow-lg">
                                정답 제출
                            </button>
                            <p id="quiz-feedback" class="mt-4 text-xl font-bold"></p>
                        </div>
                    </main>
                </div>
            `;
            
            return html;
        }
        
        // NEW: Handles the selection highlighting
        function handleSelection(selectedInput) {
            // Find all sibling spans (quiz options) and remove the checked style
            const allOptions = document.querySelectorAll('.quiz-option span');
            allOptions.forEach(span => {
                span.style.backgroundColor = ''; // Reset background
                span.style.color = '#1e293b'; // Reset text color
                span.style.borderColor = '#e5e7eb'; // Reset border color
                span.style.boxShadow = ''; // Reset shadow
                span.style.transform = ''; // Reset scale
            });

            // Re-apply the selection style only to the currently checked item's sibling span
            const selectedSpan = selectedInput.nextElementSibling;
            if (selectedSpan) {
                selectedSpan.style.backgroundColor = '#f7a94a'; // Selection color (Orange)
                selectedSpan.style.color = 'white';
                selectedSpan.style.borderColor = '#f7a94a';
                selectedSpan.style.boxShadow = '0 4px 6px -1px rgba(247, 169, 74, 0.5), 0 2px 4px -2px rgba(247, 169, 74, 0.5)';
                selectedSpan.style.transform = 'scale(1.02)';
            }
            
            // Clear feedback and reset button state if it was previously incorrect
            document.getElementById('quiz-feedback').textContent = '';
            document.getElementById('submit-button').disabled = false;
        }


        function checkFinalAnswer() {
            const feedback = document.getElementById('quiz-feedback');
            const currentQ = finalQuizQuestions[masterQuizStage];
            const submitButton = document.getElementById('submit-button');
            
            // Get selected radio button value
            const selectedInput = document.querySelector('input[name="quiz-answer"]:checked');
            
            if (!selectedInput) {
                feedback.textContent = `⚠️ 정답을 선택해 주세요!`;
                feedback.className = 'mt-4 text-xl font-bold text-yellow-600';
                return;
            }

            const userAnswer = selectedInput.value.trim();
            const correctAnswer = currentQ.a.trim();

            // Reset all option styles first
            document.querySelectorAll('.quiz-option').forEach(span => {
                span.classList.remove('correct', 'incorrect');
                // Re-apply the 'selected' style if checked
                if (span.previousElementSibling && span.previousElementSibling.checked) {
                    handleSelection(span.previousElementSibling); 
                } else {
                    span.style.backgroundColor = 'white'; 
                    span.style.color = '#1e293b'; 
                    span.style.borderColor = '#e5e7eb';
                    span.style.boxShadow = '';
                    span.style.transform = '';
                }
            });
            
            const selectedSpan = selectedInput.nextElementSibling;

            if (userAnswer === correctAnswer) {
                // CORRECT: Highlight green and proceed
                selectedSpan.classList.add('correct');
                selectedSpan.style.boxShadow = '0 4px 6px -1px rgba(16, 185, 129, 0.5), 0 2px 4px -2px rgba(16, 185, 129, 0.5)';
                
                feedback.textContent = `✅ Stage ${masterQuizStage + 1} 통과! 다음 스테이지로 이동합니다.`;
                feedback.className = 'mt-4 text-xl font-bold text-green-600';
                
                // Disable all radio buttons to prevent further attempts on this question
                document.querySelectorAll('input[name="quiz-answer"]').forEach(input => input.disabled = true);
                submitButton.disabled = true;

                masterQuizStage++;
                
                if (masterQuizStage === finalQuizQuestions.length) {
                    // All 5 stages completed
                    setTimeout(showMasterAnimation, 2000);
                } else {
                    // Advance to next stage
                    setTimeout(() => {
                        // Dramatic transition for in-quiz stage change
                        const quizWrapper = document.querySelector('.quiz-wrapper');
                        if (quizWrapper) {
                            quizWrapper.classList.add('page-exit');
                            setTimeout(() => {
                                document.body.innerHTML = renderFinalQuiz();
                                const newQuizWrapper = document.querySelector('.quiz-wrapper');
                                if (newQuizWrapper) {
                                    requestAnimationFrame(() => {
                                        requestAnimationFrame(() => {
                                            newQuizWrapper.classList.add('ready');
                                        });
                                    });
                                }
                            }, 1000); // Wait for exit animation
                        }
                    }, 2000);
                }

            } else {
                // INCORRECT: Highlight red, clear selection, and allow re-try
                selectedSpan.classList.add('incorrect');
                
                feedback.textContent = `❌ 아쉽습니다. 다시 한번 생각해 보고 선택해 주세요.`;
                feedback.className = 'mt-4 text-xl font-bold text-red-600';
                
                // Uncheck the radio button to reset state
                selectedInput.checked = false;
                
                // After a short delay, reset the visual style of the incorrect selection
                setTimeout(() => {
                    selectedSpan.style.backgroundColor = 'white'; 
                    selectedSpan.style.color = '#1e293b'; 
                    selectedSpan.style.borderColor = '#e5e7eb';
                    selectedSpan.style.boxShadow = '';
                    selectedSpan.style.transform = '';
                    
                    feedback.textContent = ''; // Clear feedback text
                }, 1500); 
            }
        }


        function showMasterAnimation() {
            document.body.innerHTML = `
                <div class="master-overlay flex flex-col items-center justify-center min-h-screen text-center p-8 bg-gradient-to-br from-yellow-100 to-yellow-300">
                    <div class="animate-confetti-burst">
                        <p class="text-8xl mb-8 animate-pulse">👑🎉</p>
                    </div>
                    <h1 class="text-7xl md:text-8xl jua-font text-red-700 mb-6 font-extrabold animate-title-reveal">
                        ✨ 풍습 마스터 ✨
                    </h1>
                    <p class="text-3xl text-dark-accent font-semibold mb-10 animate-fade-in-up">
                        모든 학습과 최종 퀴즈를 완벽하게 통과하셨습니다!
                    </p>
                    <button onclick="window.location.reload()" class="bg-dark-accent hover:bg-[#523f33] text-white text-2xl font-bold py-4 px-10 rounded-full shadow-2xl transition duration-300 transform hover:scale-110">
                        처음으로 돌아가기
                    </button>
                </div>
            `;
        }

        // Function to generate the HTML content for a single face (Past or Present)
        function generateFaceContent(data, type) {
            let currentText = data.text;
            let blankCounter = 0;

            const parsedText = currentText.replace(/\[(\d+)\]/g, (match, index) => {
                const answer = data.answers[blankCounter];
                const blankId = index; // Use the global index from [1] to [28]

                blankCounter++; 

                return `
                    <span class="relative whitespace-nowrap">
                        <input 
                            type="text" 
                            id="blank-${blankId}"
                            class="blank-input focus:outline-none focus:ring-2 focus:ring-dark-accent" 
                            data-answer-id="${blankId}"
                            data-correct-answer="${answer.trim()}"
                            onblur="instantCheck(this)"
                            onkeyup="if(event.key === 'Enter') instantCheck(this);"
                            oninput="adjustInputWidth(this);"
                            onclick="event.stopPropagation()"
                        />
                        <!-- Answer span is hidden but kept for legacy -->
                        <span id="answer-${blankId}" class="blank-answer">${answer}</span>
                    </span>
                `;
            });

            // 태그 색상 변경 적용
            const tagClass = type === '과거' ? 'bg-past-accent-light text-past-accent' : 'bg-present-accent-light text-present-accent';

            return `
                <div class="flex items-center space-x-3 mb-2">
                    <span class="text-lg font-semibold p-1 px-3 rounded-full ${tagClass}">${type}</span>
                    <p class="text-gray-500 text-sm">(${type}의 모습)</p>
                </div>
                <p class="text-lg text-gray-800 leading-relaxed card-face-content">${parsedText}</p>
            `;
        }

        // Function to render a single flippable topic card
        function renderTopicCard(topic) {
            const innerId = `card-inner-${topic.idPrefix}`;
            return `
                <div class="flip-card-container h-auto min-h-[250px] md:min-h-[300px] w-full" onclick="flipCard(document.getElementById('${innerId}'))">
                    <div id="${innerId}" class="flip-card-inner cursor-pointer">
                        <!-- Card Front (Past) -->
                        <div class="card-face card-front">
                            <h2 class="text-3xl font-extrabold text-past-accent">${topic.title} ${topic.emoji}</h2>
                            ${generateFaceContent(topic.past, '과거')}
                            <p class="text-lg font-extrabold text-dark-accent mt-4 text-center animate-pulse">👆 클릭하여 오늘날의 모습 확인!</p>
                        </div>
                        <!-- Card Back (Present) -->
                        <div class="card-face card-back">
                            <h2 class="text-3xl font-extrabold text-present-accent">${topic.title} ${topic.emoji}</h2>
                            ${generateFaceContent(topic.present, '오늘날')}
                            <p class="text-sm text-gray-500 mt-4 text-center">클릭하여 과거의 모습 확인</p>
                        </div>
                    </div>
                </div>
            `;
        }

        // Function to render a single static section
        function renderStaticSection(sectionData) {
            const qData = sectionData.data;
            let currentText = qData.text;
            let blankCounter = 0;
            
            // Need to find the start of the blank index for this section (ID 9, 10, 11)
            let blankOffset = allQuestions.slice(0, qData.id - 1).reduce((sum, q) => sum + q.answers.length, 0);
            
            const parsedText = currentText.replace(/\[(\d+)\]/g, (match, index) => {
                const answer = qData.answers[blankCounter];
                // index is the global blank index, but we use blankOffset to accurately map to the correct answer.
                const blankId = blankOffset + (++blankCounter);

                return `
                    <span class="relative whitespace-nowrap">
                        <input 
                            type="text" 
                            id="blank-${blankId}"
                            class="blank-input focus:outline-none focus:ring-2 focus:ring-dark-accent" 
                            data-answer-id="${blankId}"
                            data-correct-answer="${answer.trim()}"
                            onblur="instantCheck(this)"
                            onkeyup="if(event.key === 'Enter') instantCheck(this);"
                            oninput="adjustInputWidth(this);"
                        />
                        <!-- Answer span is hidden but kept for legacy -->
                        <span id="answer-${blankId}" class="blank-answer">${answer}</span>
                    </span>
                `;
            });

            // 정적인 섹션의 배경색 및 테두리 색상 변경
            const bgColor = qData.title === '핵심 정리' ? 'bg-past-accent-light' : 'bg-white';
            const borderColor = qData.title === '핵심 정리' ? 'border-[#f08080]' : 'border-[#695241]';

            return `
                <div class="${bgColor} p-6 rounded-xl shadow-lg border-t-4 ${borderColor}">
                    <h2 class="text-2xl font-bold text-dark-accent mb-2">${qData.section}</h2>
                    <h3 class="text-xl font-semibold text-gray-800 mb-3">${qData.title} ${sectionData.emoji}</h3>
                    ${qData.id === 9 ? '<p class="text-gray-500 mb-4">옛날 사람들은 주로 농사를 지으며 살았습니다. 그래서 농사가 잘되고 사람들이 건강하게 살기를 바라는 마음을 담아 계절이나 명절에 따라 다양한 풍습을 지켰습니다. 반면 오늘날에는 농사와 관련된 풍습이 많이 사라지고, 설날과 추석 등의 명절을 중심으로 세시 풍속이 이어지고 있습니다.</p>' : ''}
                    <p class="text-lg text-gray-700 leading-relaxed">${parsedText}</p>
                </div>
            `;
        }

        // Function to render all content
        function renderApp() {
            const container = document.getElementById('app-container');
            let contentHtml = '<div class="grid md:grid-cols-2 gap-6">';

            // Render flippable topics
            topicGroups.forEach(topic => {
                contentHtml += renderTopicCard(topic);
            });
            contentHtml += '</div>'; // Close grid

            // Render static sections
            staticSections.forEach(section => {
                contentHtml += renderStaticSection(section);
            });
            
            container.innerHTML = contentHtml;
            
            // Initial input width adjustment (must be done after element creation)
            document.querySelectorAll('.blank-input').forEach(adjustInputWidth);
            // Initial progress update (should be 0/28)
            updateProgress(0);
        }


        // Initialize the application on window load
        window.onload = renderApp;
    </script>
</body>
</html>        }
        
        /* Answer display logic (Not used anymore but keeping structure) */
        .blank-answer {
            color: #1d4ed8; 
            font-weight: 700;
            display: none;
        }

        /* Card Flip Styles */
        .flip-card-container {
            perspective: 1000px;
        }
        .flip-card-inner {
            transition: transform 0.8s;
            transform-style: preserve-3d;
            height: 100%;
            position: relative;
        }
        .flip-card-inner.flipped {
            transform: rotateY(180deg);
        }
        .card-face {
            position: absolute;
            width: 100%;
            height: 100%;
            backface-visibility: hidden;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            padding: 1.5rem;
            border-radius: 0.75rem;
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
            min-height: 250px; 
            background-color: #ffffff; /* 카드 배경은 흰색 유지 */
        }
        .card-front {
            border-top: 4px solid #f08080; /* 과거 Accent (산호색) */
        }
        .card-back {
            border-top: 4px solid #72c262; /* 오늘날 Accent (녹색) */
            transform: rotateY(180deg);
        }

        /* --- Dramatic Page Transition Styles --- */
        .page-transition {
            transition: opacity 1.2s ease-in-out, transform 1.2s ease-in-out;
        }
        
        /* Style for the screen to dramatically exit */
        .page-exit {
            opacity: 0 !important;
            transform: scale(0.5) rotateX(15deg) !important;
        }
        
        /* Style for the new quiz screen to dramatically enter */
        .page-enter {
            opacity: 0;
            transform: scale(1.3);
        }
        .page-enter.ready {
            opacity: 1;
            transform: scale(1);
            transition: opacity 1s ease-out, transform 1s ease-out;
        }
        
        /* Custom radio button style for Quiz (IMPROVED for selection visibility) */
        .quiz-option {
            background-color: #ffffff;
            border: 2px solid #e5e7eb;
            transition: all 0.2s;
            color: #1e293b; /* Default text color */
        }
        .quiz-option:hover {
            background-color: #f3f4f6;
            border-color: #695241;
        }
        
        /* State when the radio button is CHECKED */
        .quiz-option input[type="radio"]:checked + span {
            background-color: #f7a94a; /* Selecting color: Orange */
            color: white;
            border-color: #f7a94a;
            box-shadow: 0 4px 6px -1px rgba(247, 169, 74, 0.5), 0 2px 4px -2px rgba(247, 169, 74, 0.5);
            transform: scale(1.02);
        }
        
        /* State when the answer is CORRECT (Green) */
        .quiz-option.correct {
            background-color: #10b981; 
            color: white;
            border-color: #10b981;
            transform: scale(1.02);
        }
        
        /* State when the answer is INCORRECT (Red) */
        .quiz-option.incorrect {
            background-color: #ef4444; 
            color: white;
            border-color: #ef4444;
        }
        
        /* Quiz title animation */
        @keyframes bounce {
            0%, 100% { transform: translateY(-5%); }
            50% { transform: translateY(0); }
        }
        .animate-bounce-stage {
            animation: bounce 1s infinite;
        }
    </style>
</head>
<!-- Initial Body styling for smooth transition -->
<body class="bg-hanji min-h-screen p-4 md:p-8 page-transition">

    <!-- Header - Updated for traditional colors -->
    <header class="text-center mb-8">
        <h1 class="text-5xl font-bold mb-4 jua-font text-dark-accent">
            ⭐ 옛날과 오늘날의 풍습 비교 학습 ⭐
        </h1>
        <p class="text-xl text-white bg-dark-accent inline-block py-2 px-4 rounded-full font-extrabold shadow-lg transition duration-300 transform hover:scale-105">
            카드를 눌러 풍습의 변화를 확인하고, 빈칸을 채워보세요! 👀
        </p>
    </header>
    
    <!-- Progress Bar Section (Sticky) -->
    <div id="progress-container" class="sticky top-0 z-10 bg-hanji/95 p-3 rounded-lg shadow-xl border-b-4 border-dark-accent mb-6 backdrop-blur-sm">
        <h2 class="text-lg font-bold text-dark-accent mb-1">진행도: <span id="progress-text">0/28 (0%)</span></h2>
        <div class="w-full h-4 bg-gray-300 rounded-full overflow-hidden">
            <div id="progress-bar" class="h-full bg-red-400 rounded-full transition-all duration-500 ease-out shadow-inner" style="width: 0%;"></div>
        </div>
    </div>

    <main id="app-container" class="max-w-4xl mx-auto space-y-8">
        <!-- Topic Cards and Static Sections will be rendered here by JavaScript -->
    </main>
    
    <!-- NEW: Master Quiz Force Start Button -->
    <div class="max-w-4xl mx-auto p-4 text-center mt-6">
        <button id="force-start-button" onclick="checkCompletionAndStartQuiz(true)" 
                class="bg-blue-600 hover:bg-blue-700 text-white font-bold py-3 px-6 rounded-full shadow-xl transition duration-300 transform hover:scale-105">
            🚀 마스터 퀴즈 바로 시작하기 (테스트용)
        </button>
    </div>

    <!-- Modal for messages -->
    <div id="message-modal" class="fixed inset-0 bg-gray-600 bg-opacity-50 hidden items-center justify-center p-4 z-50">
        <div class="bg-white rounded-xl shadow-2xl p-6 max-w-sm w-full">
            <h3 id="modal-title" class="text-xl font-semibold mb-3 text-dark-accent">알림</h3>
            <p id="modal-text" class="text-gray-700 mb-4">메시지 내용</p>
            <button onclick="closeModal()" class="w-full bg-dark-accent hover:bg-[#523f33] text-white font-bold py-2 px-4 rounded-lg transition duration-200">확인</button>
        </div>
    </div>

    <script>
        // Original Data Structure
        const allQuestions = [
            { id: 1, section: '1. 일상생활 속 풍습의 변화', title: '1-1. 돌잔치', type: '과거', 
              text: '옛날에는 아기가 태어난 지 [1]이 되면 아이의 건강을 축하하는 의미로 [2]를 하였습니다.', 
              answers: ['1년', '돌잔치'] },
            { id: 2, section: '1. 일상생활 속 풍습의 변화', title: '1-1. 돌잔치', type: '오늘날', 
              text: '오늘날에는 돌잔치를 [3] 하거나 간소하게 진행하기도 합니다. 직업의 다양화로 [4]에 사용되는 물건도 새로 생겨났습니다.', 
              answers: ['안', '돌잡이'] },
            { id: 3, section: '1. 일상생활 속 풍습의 변화', title: '1-2. 결혼식', type: '과거', 
              text: '[5]에서 정해 준 상대와 결혼하였으며, [6] 집에서 [7] [8]을 입고 결혼식을 올린 뒤, 나중에 [9] 집으로 가서 살았습니다.', 
              answers: ['집안', '신부', '전통', '한복', '신랑'] },
            { id: 4, section: '1. 일상생활 속 풍습의 변화', title: '1-2. 결혼식', type: '오늘날', 
              text: '결혼식 형식이 [10]해졌으며, 결혼식 과정도 개인의 [11]에 따라 달라졌습니다.', 
              answers: ['다양', '선택'] },
            { id: 5, section: '1. 일상생활 속 풍습의 변화', title: '1-3. 장례식', type: '과거', 
              text: '돌아가신 분을 땅에 묻고 [12]일이나 [13]일 동안 장례를 치렀습니다. 이후 시기와 때를 맞춰 [14]하고 [15]를 지냈습니다.', 
              answers: ['5', '7', '성묘', '제사'] },
            { id: 6, section: '1. 일상생활 속 풍습의 변화', title: '1-3. 장례식', type: '오늘날', 
              text: '오늘날에는 주로 [16]일 동안 장례를 치릅니다. 돌아가신 분은 [17]하여 [18]에 모시는 경우가 점점 많아지고, [19]을 간단하게 차리기도 합니다.', 
              answers: ['3', '화장', '납골당', '제사상'] },
            { id: 7, section: '1. 일상생활 속 풍습의 변화', title: '1-4. 놀이', type: '과거', 
              text: '[20]에서 사람들과 함께하는 놀이가 많았습니다.', 
              answers: ['자연'] },
            { id: 8, section: '1. 일상생활 속 풍습의 변화', title: '1-4. 놀이', type: '오늘날', 
              text: '[21]이나 [22]를 이용해 친구들과 게임을 즐깁니다.', 
              answers: ['스마트폰', '컴퓨터'] },
            { id: 9, section: '2. 세시 풍속의 변화', title: '세시 풍속의 의미', type: '과거', 
              text: '옛날 사람들은 주로 농사를 지으며 살았습니다. 그래서 [23]가 잘되고 사람들이 [24]하게 살기를 바라는 마음을 담아 계절이나 명절에 따라 다양한 풍습을 지켰습니다.', 
              answers: ['농사', '건강'] },
            { id: 10, section: '2. 세시 풍속의 변화', title: '2. 세시 풍속의 변화', type: '오늘날', 
              text: '오늘날의 풍습은 옛날과 달라졌지만, 가족이 함께 모여 음식을 만들고 서로의 [25]과 [26]을 바라는 마음은 오늘날에도 계속되고 있습니다.', 
              answers: ['건강', '행복'] },
            { id: 11, section: '변화 정리', title: '핵심 정리', type: '요약', 
              text: '→ 오늘날에는 각자의 선택에 따라 풍습이 [27]해졌으며, 옛날보다 과정이나 형식이 [28]해졌습니다.', 
              answers: ['다양', '간단'] }
        ];

        // Group data into flippable topics
        const topicGroups = [
            { title: '돌잔치', idPrefix: 'doljanchi', past: allQuestions.find(q => q.id === 1), present: allQuestions.find(q => q.id === 2), emoji: '👶🎂' },
            { title: '결혼식', idPrefix: 'wedding', past: allQuestions.find(q => q.id === 3), present: allQuestions.find(q => q.id === 4), emoji: '💍🎎' },
            { title: '장례식', idPrefix: 'funeral', past: allQuestions.find(q => q.id === 5), present: allQuestions.find(q => q.id === 6), emoji: '🕯️🙏' },
            { title: '놀이', idPrefix: 'play', past: allQuestions.find(q => q.id === 7), present: allQuestions.find(q => q.id === 8), emoji: '🎮⚽' },
        ];

        // Static content sections
        const staticSections = [
            { data: allQuestions.find(q => q.id === 9), emoji: '🌾🗓️' }, // 세시 풍속
            { data: allQuestions.find(q => q.id === 10), emoji: '👨‍👩‍👧‍👦💖' }, // 세시 풍속 변화
            { data: allQuestions.find(q => q.id === 11), emoji: '💡✨' }, // 핵심 정리
        ];

        // --- NEW GLOBAL STATE & CONSTANTS FOR QUIZ ---
        const TOTAL_BLANKS = allQuestions.reduce((sum, q) => sum + q.answers.length, 0); // Total 28 blanks
        let isMasterQuizActive = false;
        let masterQuizStage = 0;

        // NEW: 객관식/OX로 구성된 최종 퀴즈 문제 목록
        const finalQuizQuestions = [
            { 
                type: 'OX', 
                q: "옛날에는 아기가 태어난 지 1년이 되는 날, 돌잔치를 열어 건강을 축하했습니다. (O/X)", 
                options: ["O", "X"],
                a: "O" 
            },
            { 
                type: 'MCQ', 
                q: "옛날 결혼식에서, 결혼식을 올린 뒤 신랑 집으로 가서 살았던 사람은?", 
                options: ["신랑", "신부", "중매쟁이", "주례사"], 
                a: "신부" 
            },
            { 
                type: 'MCQ', 
                q: "오늘날 장례 풍습에 대한 설명으로 옳은 것은?", 
                options: [
                    "① 돌아가신 분을 땅에 묻는 매장 방식이 대부분이다.",
                    "② 장례 기간은 보통 옛날과 같이 5일이나 7일 동안 치러진다.",
                    "③ 돌아가신 분을 화장하여 납골당에 모시는 경우가 많다.",
                    "④ 제사는 반드시 옛 방식대로 복잡하게 차려야 한다."
                ], 
                a: "③ 돌아가신 분을 화장하여 납골당에 모시는 경우가 많다."
            },
            { 
                type: 'OX', 
                q: "오늘날의 놀이 풍습은 옛날처럼 자연에서 사람들과 함께하는 놀이가 주를 이룹니다. (O/X)", 
                options: ["O", "X"],
                a: "X" 
            },
            { 
                type: 'MCQ', 
                q: "오늘날 풍습 변화의 핵심 특징으로 가장 알맞은 것은?", 
                options: [
                    "① 모두 전통 한복을 입고 행사를 진행해야 한다.",
                    "② 과정이나 형식이 옛날보다 훨씬 복잡해졌다.",
                    "③ 각자의 선택에 따라 다양해졌으며, 과정이 간단해졌다.",
                    "④ 오직 가족 단위로만 행사를 치러야 한다."
                ], 
                a: "③ 각자의 선택에 따라 다양해졌으며, 과정이 간단해졌다."
            }
        ];


        // Utility to show custom modal instead of alert()
        function showModal(title, text) {
            const modal = document.getElementById('message-modal');
            document.getElementById('modal-title').textContent = title;
            document.getElementById('modal-text').textContent = text;
            modal.classList.remove('hidden');
            modal.classList.add('flex');
        }

        function closeModal() {
            const modal = document.getElementById('message-modal');
            modal.classList.add('hidden');
            modal.classList.remove('flex');
        }

        // Function to dynamically adjust input width based on content
        function adjustInputWidth(input) {
            const textWidth = input.value.length * 15 + 20; 
            input.style.width = Math.min(Math.max(textWidth, 60), 200) + 'px';
        }

        // Function to handle card click (flip)
        function flipCard(cardInnerElement) {
            if (isMasterQuizActive) return; // Cannot flip if master quiz is active
            cardInnerElement.classList.toggle('flipped');
        }
        
        // --- NEW FUNCTIONS FOR PROGRESS AND COMPLETION ---

        function updateProgress(correctCount) {
            const percentage = Math.round((correctCount / TOTAL_BLANKS) * 100);
            const progressBar = document.getElementById('progress-bar');
            const progressText = document.getElementById('progress-text');
            const forceStartButton = document.getElementById('force-start-button');

            if (progressBar && progressText) {
                progressBar.style.width = `${percentage}%`;
                progressText.textContent = `${correctCount}/${TOTAL_BLANKS} (${percentage}%)`;
                
                // Progress color change effect
                if (percentage < 33) {
                    progressBar.className = 'h-full rounded-full transition-all duration-500 ease-out shadow-inner bg-red-400';
                } else if (percentage < 66) {
                    progressBar.className = 'h-full rounded-full transition-all duration-500 ease-out shadow-inner bg-yellow-400';
                } else if (percentage < 100) {
                    progressBar.className = 'h-full rounded-full transition-all duration-500 ease-out shadow-inner bg-blue-400';
                } else {
                    // 100% completion color
                    progressBar.className = 'h-full rounded-full transition-all duration-500 ease-out bg-green-500 shadow-xl shadow-green-300';
                }
            }

            // Hide the force start button if 100% completed naturally
            if (percentage === 100 && forceStartButton) {
                 forceStartButton.style.display = 'none';
            }
        }

        function instantCheck(input) {
            if (isMasterQuizActive) return;

            const correctAnswer = input.dataset.correctAnswer;
            const userAnswer = input.value.trim();
            
            input.classList.remove('correct', 'incorrect');
            input.style.borderColor = '#9ca3af'; // Reset border color for instant feedback

            if (userAnswer === '') {
                // Do not mark as incorrect if empty, just reset style
            } else {
                // Case-insensitive comparison
                if (userAnswer.toLowerCase() === correctAnswer.toLowerCase()) {
                    input.classList.add('correct');
                } else {
                    input.classList.add('incorrect');
                }
            }
            
            // Recalculate Total Correct and Check Completion
            const allInputs = document.querySelectorAll('.blank-input');
            let currentCorrect = 0;
            
            allInputs.forEach(i => {
                if (i.classList.contains('correct')) {
                    currentCorrect++;
                }
            });
            
            updateProgress(currentCorrect);
            
            if (currentCorrect === TOTAL_BLANKS) {
                // Small delay to let the final correct color show up
                setTimeout(() => checkCompletionAndStartQuiz(false), 500);
            }
        }

        /**
         * Checks completion and starts the quiz.
         * @param {boolean} force - If true, starts the quiz regardless of completion status.
         */
        function checkCompletionAndStartQuiz(force) {
            if (isMasterQuizActive) return;

            if (!force) {
                // Check if all blanks are filled correctly (Only proceed if not forced)
                const allInputs = document.querySelectorAll('.blank-input');
                let currentCorrect = 0;
                allInputs.forEach(i => {
                    if (i.classList.contains('correct')) {
                        currentCorrect++;
                    }
                });
                if (currentCorrect !== TOTAL_BLANKS) {
                    showModal("⚠️ 아직 학습 중", "모든 빈칸을 정확하게 채워야 마스터 퀴즈가 시작됩니다! 빈칸을 마저 채워주세요. (강제 시작 버튼을 누르셨다면, 테스트가 바로 시작됩니다.)");
                    return;
                }
                showModal("✅ 100% 달성!", "축하합니다! 모든 빈칸을 채우셨습니다. 이제 '풍습 마스터' 퀴즈에 도전하세요!");
            } else {
                showModal("🚀 마스터 퀴즈 시작!", "테스트 버튼으로 최종 퀴즈를 시작합니다!");
            }

            isMasterQuizActive = true;
            
            // 1. Dramatic screen transition: Apply exit style to the current body
            document.body.classList.add('page-exit');

            // 2. Wait for the exit animation to complete (1200ms)
            setTimeout(() => {
                
                // 3. Reset body style and replace content with the quiz HTML
                document.body.classList.remove('page-exit');
                document.body.classList.add('page-transition'); 
                document.body.innerHTML = renderFinalQuiz();
                
                // 4. Trigger the entrance animation
                const quizContainer = document.querySelector('.quiz-wrapper');
                requestAnimationFrame(() => {
                    requestAnimationFrame(() => {
                        if (quizContainer) {
                            quizContainer.classList.add('ready');
                        }
                    });
                });
                
            }, 1200); 
        }
        
        function renderFinalQuiz() {
            const currentQ = finalQuizQuestions[masterQuizStage];
            
            let optionsHtml = '';
            
            // Generate HTML for options (MCQ or OX)
            optionsHtml = currentQ.options.map((option, index) => {
                // Use a generic index 'i' for mapping for clean HTML
                const inputId = `quiz-opt-${masterQuizStage}-${index}`; 
                return `
                    <label for="${inputId}" class="flex items-center space-x-3 mb-3 cursor-pointer">
                        <!-- Use radio button's checked state to style the sibling span -->
                        <input type="radio" id="${inputId}" name="quiz-answer" value="${option.trim()}" class="hidden" 
                            onchange="handleSelection(this)" />
                        <span class="quiz-option flex-1 block p-3 rounded-xl text-lg font-medium text-gray-700 hover:text-dark-accent 
                            ${currentQ.type === 'OX' ? 'text-3xl font-extrabold' : ''}">
                            ${option}
                        </span>
                    </label>
                `;
            }).join('');
            
            // Clear any old selection highlight classes on the options container
            document.querySelectorAll('.quiz-option').forEach(el => el.classList.remove('correct', 'incorrect'));


            // Wrap the entire new page content in a div with transition classes
            let html = `
                <div class="quiz-wrapper page-transition page-enter bg-hanji min-h-screen p-4 md:p-8">
                    <header class="text-center mb-12 p-8 pt-12">
                        <h1 class="text-5xl md:text-6xl font-extrabold jua-font text-red-600 mb-4 animate-bounce-stage">
                            Stage ${masterQuizStage + 1} / ${finalQuizQuestions.length}
                        </h1>
                        <p class="text-2xl text-dark-accent font-semibold">✨ 풍습 마스터 퀴즈 도전! ✨</p>
                    </header>
                    <main class="max-w-xl mx-auto p-8 rounded-2xl shadow-2xl bg-white border-8 border-yellow-500">
                        <div id="quiz-content">
                            <p class="text-2xl font-bold text-gray-700 mb-6">${currentQ.q}</p>
                            
                            <div id="quiz-options" class="space-y-4">
                                ${optionsHtml}
                            </div>
                            
                            <button id="submit-button" onclick="checkFinalAnswer()" class="w-full mt-8 bg-blue-500 hover:bg-blue-600 text-white text-xl font-bold py-3 rounded-xl transition shadow-lg">
                                정답 제출
                            </button>
                            <p id="quiz-feedback" class="mt-4 text-xl font-bold"></p>
                        </div>
                    </main>
                </div>
            `;
            
            return html;
        }
        
        // NEW: Handles the selection highlighting
        function handleSelection(selectedInput) {
            // Find all sibling spans (quiz options) and remove the checked style
            const allOptions = document.querySelectorAll('.quiz-option span');
            allOptions.forEach(span => {
                span.style.backgroundColor = ''; // Reset background
                span.style.color = '#1e293b'; // Reset text color
                span.style.borderColor = '#e5e7eb'; // Reset border color
                span.style.boxShadow = ''; // Reset shadow
                span.style.transform = ''; // Reset scale
            });

            // Re-apply the selection style only to the currently checked item's sibling span
            const selectedSpan = selectedInput.nextElementSibling;
            if (selectedSpan) {
                selectedSpan.style.backgroundColor = '#f7a94a'; // Selection color (Orange)
                selectedSpan.style.color = 'white';
                selectedSpan.style.borderColor = '#f7a94a';
                selectedSpan.style.boxShadow = '0 4px 6px -1px rgba(247, 169, 74, 0.5), 0 2px 4px -2px rgba(247, 169, 74, 0.5)';
                selectedSpan.style.transform = 'scale(1.02)';
            }
            
            // Clear feedback and reset button state if it was previously incorrect
            document.getElementById('quiz-feedback').textContent = '';
            document.getElementById('submit-button').disabled = false;
        }


        function checkFinalAnswer() {
            const feedback = document.getElementById('quiz-feedback');
            const currentQ = finalQuizQuestions[masterQuizStage];
            const submitButton = document.getElementById('submit-button');
            
            // Get selected radio button value
            const selectedInput = document.querySelector('input[name="quiz-answer"]:checked');
            
            if (!selectedInput) {
                feedback.textContent = `⚠️ 정답을 선택해 주세요!`;
                feedback.className = 'mt-4 text-xl font-bold text-yellow-600';
                return;
            }

            const userAnswer = selectedInput.value.trim();
            const correctAnswer = currentQ.a.trim();

            // Reset all option styles first
            document.querySelectorAll('.quiz-option').forEach(span => {
                span.classList.remove('correct', 'incorrect');
                // Re-apply the 'selected' style if checked
                if (span.previousElementSibling && span.previousElementSibling.checked) {
                    handleSelection(span.previousElementSibling); 
                } else {
                    span.style.backgroundColor = 'white'; 
                    span.style.color = '#1e293b'; 
                    span.style.borderColor = '#e5e7eb';
                    span.style.boxShadow = '';
                    span.style.transform = '';
                }
            });
            
            const selectedSpan = selectedInput.nextElementSibling;

            if (userAnswer === correctAnswer) {
                // CORRECT: Highlight green and proceed
                selectedSpan.classList.add('correct');
                selectedSpan.style.boxShadow = '0 4px 6px -1px rgba(16, 185, 129, 0.5), 0 2px 4px -2px rgba(16, 185, 129, 0.5)';
                
                feedback.textContent = `✅ Stage ${masterQuizStage + 1} 통과! 다음 스테이지로 이동합니다.`;
                feedback.className = 'mt-4 text-xl font-bold text-green-600';
                
                // Disable all radio buttons to prevent further attempts on this question
                document.querySelectorAll('input[name="quiz-answer"]').forEach(input => input.disabled = true);
                submitButton.disabled = true;

                masterQuizStage++;
                
                if (masterQuizStage === finalQuizQuestions.length) {
                    // All 5 stages completed
                    setTimeout(showMasterAnimation, 2000);
                } else {
                    // Advance to next stage
                    setTimeout(() => {
                        // Dramatic transition for in-quiz stage change
                        const quizWrapper = document.querySelector('.quiz-wrapper');
                        if (quizWrapper) {
                            quizWrapper.classList.add('page-exit');
                            setTimeout(() => {
                                document.body.innerHTML = renderFinalQuiz();
                                const newQuizWrapper = document.querySelector('.quiz-wrapper');
                                if (newQuizWrapper) {
                                    requestAnimationFrame(() => {
                                        requestAnimationFrame(() => {
                                            newQuizWrapper.classList.add('ready');
                                        });
                                    });
                                }
                            }, 1000); // Wait for exit animation
                        }
                    }, 2000);
                }

            } else {
                // INCORRECT: Highlight red, clear selection, and allow re-try
                selectedSpan.classList.add('incorrect');
                
                feedback.textContent = `❌ 아쉽습니다. 다시 한번 생각해 보고 선택해 주세요.`;
                feedback.className = 'mt-4 text-xl font-bold text-red-600';
                
                // Uncheck the radio button to reset state
                selectedInput.checked = false;
                
                // After a short delay, reset the visual style of the incorrect selection
                setTimeout(() => {
                    selectedSpan.style.backgroundColor = 'white'; 
                    selectedSpan.style.color = '#1e293b'; 
                    selectedSpan.style.borderColor = '#e5e7eb';
                    selectedSpan.style.boxShadow = '';
                    selectedSpan.style.transform = '';
                    
                    feedback.textContent = ''; // Clear feedback text
                }, 1500); 
            }
        }


        function showMasterAnimation() {
            document.body.innerHTML = `
                <div class="master-overlay flex flex-col items-center justify-center min-h-screen text-center p-8 bg-gradient-to-br from-yellow-100 to-yellow-300">
                    <div class="animate-confetti-burst">
                        <p class="text-8xl mb-8 animate-pulse">👑🎉</p>
                    </div>
                    <h1 class="text-7xl md:text-8xl jua-font text-red-700 mb-6 font-extrabold animate-title-reveal">
                        ✨ 풍습 마스터 ✨
                    </h1>
                    <p class="text-3xl text-dark-accent font-semibold mb-10 animate-fade-in-up">
                        모든 학습과 최종 퀴즈를 완벽하게 통과하셨습니다!
                    </p>
                    <button onclick="window.location.reload()" class="bg-dark-accent hover:bg-[#523f33] text-white text-2xl font-bold py-4 px-10 rounded-full shadow-2xl transition duration-300 transform hover:scale-110">
                        처음으로 돌아가기
                    </button>
                </div>
            `;
        }

        // Function to generate the HTML content for a single face (Past or Present)
        function generateFaceContent(data, type) {
            let currentText = data.text;
            let blankCounter = 0;

            const parsedText = currentText.replace(/\[(\d+)\]/g, (match, index) => {
                const answer = data.answers[blankCounter];
                const blankId = index; // Use the global index from [1] to [28]

                blankCounter++; 

                return `
                    <span class="relative whitespace-nowrap">
                        <input 
                            type="text" 
                            id="blank-${blankId}"
                            class="blank-input focus:outline-none focus:ring-2 focus:ring-dark-accent" 
                            data-answer-id="${blankId}"
                            data-correct-answer="${answer.trim()}"
                            onblur="instantCheck(this)"
                            onkeyup="if(event.key === 'Enter') instantCheck(this);"
                            oninput="adjustInputWidth(this);"
                            onclick="event.stopPropagation()"
                        />
                        <!-- Answer span is hidden but kept for legacy -->
                        <span id="answer-${blankId}" class="blank-answer">${answer}</span>
                    </span>
                `;
            });

            // 태그 색상 변경 적용
            const tagClass = type === '과거' ? 'bg-past-accent-light text-past-accent' : 'bg-present-accent-light text-present-accent';

            return `
                <div class="flex items-center space-x-3 mb-2">
                    <span class="text-lg font-semibold p-1 px-3 rounded-full ${tagClass}">${type}</span>
                    <p class="text-gray-500 text-sm">(${type}의 모습)</p>
                </div>
                <p class="text-lg text-gray-800 leading-relaxed card-face-content">${parsedText}</p>
            `;
        }

        // Function to render a single flippable topic card
        function renderTopicCard(topic) {
            const innerId = `card-inner-${topic.idPrefix}`;
            return `
                <div class="flip-card-container h-auto min-h-[250px] md:min-h-[300px] w-full" onclick="flipCard(document.getElementById('${innerId}'))">
                    <div id="${innerId}" class="flip-card-inner cursor-pointer">
                        <!-- Card Front (Past) -->
                        <div class="card-face card-front">
                            <h2 class="text-3xl font-extrabold text-past-accent">${topic.title} ${topic.emoji}</h2>
                            ${generateFaceContent(topic.past, '과거')}
                            <p class="text-lg font-extrabold text-dark-accent mt-4 text-center animate-pulse">👆 클릭하여 오늘날의 모습 확인!</p>
                        </div>
                        <!-- Card Back (Present) -->
                        <div class="card-face card-back">
                            <h2 class="text-3xl font-extrabold text-present-accent">${topic.title} ${topic.emoji}</h2>
                            ${generateFaceContent(topic.present, '오늘날')}
                            <p class="text-sm text-gray-500 mt-4 text-center">클릭하여 과거의 모습 확인</p>
                        </div>
                    </div>
                </div>
            `;
        }

        // Function to render a single static section
        function renderStaticSection(sectionData) {
            const qData = sectionData.data;
            let currentText = qData.text;
            let blankCounter = 0;
            
            // Need to find the start of the blank index for this section (ID 9, 10, 11)
            let blankOffset = allQuestions.slice(0, qData.id - 1).reduce((sum, q) => sum + q.answers.length, 0);
            
            const parsedText = currentText.replace(/\[(\d+)\]/g, (match, index) => {
                const answer = qData.answers[blankCounter];
                // index is the global blank index, but we use blankOffset to accurately map to the correct answer.
                const blankId = blankOffset + (++blankCounter);

                return `
                    <span class="relative whitespace-nowrap">
                        <input 
                            type="text" 
                            id="blank-${blankId}"
                            class="blank-input focus:outline-none focus:ring-2 focus:ring-dark-accent" 
                            data-answer-id="${blankId}"
                            data-correct-answer="${answer.trim()}"
                            onblur="instantCheck(this)"
                            onkeyup="if(event.key === 'Enter') instantCheck(this);"
                            oninput="adjustInputWidth(this);"
                        />
                        <!-- Answer span is hidden but kept for legacy -->
                        <span id="answer-${blankId}" class="blank-answer">${answer}</span>
                    </span>
                `;
            });

            // 정적인 섹션의 배경색 및 테두리 색상 변경
            const bgColor = qData.title === '핵심 정리' ? 'bg-past-accent-light' : 'bg-white';
            const borderColor = qData.title === '핵심 정리' ? 'border-[#f08080]' : 'border-[#695241]';

            return `
                <div class="${bgColor} p-6 rounded-xl shadow-lg border-t-4 ${borderColor}">
                    <h2 class="text-2xl font-bold text-dark-accent mb-2">${qData.section}</h2>
                    <h3 class="text-xl font-semibold text-gray-800 mb-3">${qData.title} ${sectionData.emoji}</h3>
                    ${qData.id === 9 ? '<p class="text-gray-500 mb-4">옛날 사람들은 주로 농사를 지으며 살았습니다. 그래서 농사가 잘되고 사람들이 건강하게 살기를 바라는 마음을 담아 계절이나 명절에 따라 다양한 풍습을 지켰습니다. 반면 오늘날에는 농사와 관련된 풍습이 많이 사라지고, 설날과 추석 등의 명절을 중심으로 세시 풍속이 이어지고 있습니다.</p>' : ''}
                    <p class="text-lg text-gray-700 leading-relaxed">${parsedText}</p>
                </div>
            `;
        }

        // Function to render all content
        function renderApp() {
            const container = document.getElementById('app-container');
            let contentHtml = '<div class="grid md:grid-cols-2 gap-6">';

            // Render flippable topics
            topicGroups.forEach(topic => {
                contentHtml += renderTopicCard(topic);
            });
            contentHtml += '</div>'; // Close grid

            // Render static sections
            staticSections.forEach(section => {
                contentHtml += renderStaticSection(section);
            });
            
            container.innerHTML = contentHtml;
            
            // Initial input width adjustment (must be done after element creation)
            document.querySelectorAll('.blank-input').forEach(adjustInputWidth);
            // Initial progress update (should be 0/28)
            updateProgress(0);
        }


        // Initialize the application on window load
        window.onload = renderApp;
    </script>
</body>
</html>
