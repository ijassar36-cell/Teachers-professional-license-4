<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>محاكي اختبار الرخصة المهنية للمعلمين</title>
    <style>
        :root {
            --primary-color: #1a1a2e;
            --secondary-color: #16213e;
            --accent-color: #0f3460;
            --correct-color: #2ecc71;
            --incorrect-color: #e74c3c;
            --text-color: #ecf0f1;
            --border-radius: 10px;
            --transition: all 0.3s ease;
            --card-shadow: 0 8px 16px rgba(0, 0, 0, 0.3);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background: linear-gradient(135deg, var(--primary-color), #0c0c1a);
            color: var(--text-color);
            line-height: 1.6;
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
        }

        header {
            text-align: center;
            margin-bottom: 30px;
            padding: 25px;
            background-color: var(--secondary-color);
            border-radius: var(--border-radius);
            box-shadow: var(--card-shadow);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        h1 {
            font-size: 2.5rem;
            margin-bottom: 15px;
            color: #4cc9f0;
            text-shadow: 0 2px 4px rgba(0, 0, 0, 0.5);
        }

        .subtitle {
            font-size: 1.2rem;
            color: #b0b0b0;
            margin-bottom: 10px;
        }

        .exam-info {
            display: flex;
            justify-content: space-between;
            background-color: var(--secondary-color);
            padding: 20px;
            border-radius: var(--border-radius);
            margin-bottom: 25px;
            box-shadow: var(--card-shadow);
            flex-wrap: wrap;
            gap: 15px;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        .info-item {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .info-item i {
            color: #4cc9f0;
            font-size: 1.2rem;
        }

        .progress-container {
            margin-bottom: 25px;
            background-color: var(--secondary-color);
            padding: 15px;
            border-radius: var(--border-radius);
            box-shadow: var(--card-shadow);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        .progress-bar {
            height: 12px;
            background-color: rgba(255, 255, 255, 0.1);
            border-radius: 6px;
            overflow: hidden;
        }

        .progress {
            height: 100%;
            background: linear-gradient(90deg, #4cc9f0, #4361ee);
            border-radius: 6px;
            transition: width 0.5s ease;
            width: 0%;
        }

        .progress-text {
            display: flex;
            justify-content: space-between;
            margin-top: 8px;
            font-size: 0.9rem;
            color: #b0b0b0;
        }

        .question-container {
            background-color: var(--secondary-color);
            border-radius: var(--border-radius);
            padding: 25px;
            margin-bottom: 25px;
            box-shadow: var(--card-shadow);
            transition: var(--transition);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        .question-header {
            display: flex;
            justify-content: space-between;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
        }

        .question-number {
            font-weight: bold;
            color: #4cc9f0;
            font-size: 1.2rem;
        }

        .question-text {
            font-size: 1.15rem;
            margin-bottom: 25px;
            line-height: 1.8;
            background-color: rgba(0, 0, 0, 0.2);
            padding: 15px;
            border-radius: var(--border-radius);
            border-right: 3px solid #4cc9f0;
        }

        .options-container {
            display: grid;
            grid-template-columns: 1fr;
            gap: 15px;
            margin-bottom: 20px;
        }

        .option {
            padding: 18px;
            background-color: rgba(255, 255, 255, 0.05);
            border-radius: var(--border-radius);
            cursor: pointer;
            transition: var(--transition);
            border: 1px solid rgba(255, 255, 255, 0.1);
            display: flex;
            align-items: center;
            position: relative;
        }

        .option:hover {
            background-color: rgba(255, 255, 255, 0.1);
            transform: translateY(-3px);
            box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
        }

        .option.disabled {
            cursor: not-allowed;
            opacity: 0.7;
        }

        .option.disabled:hover {
            transform: none;
            box-shadow: none;
        }

        .option-label {
            font-weight: bold;
            margin-left: 15px;
            width: 35px;
            height: 35px;
            display: flex;
            align-items: center;
            justify-content: center;
            background-color: rgba(255, 255, 255, 0.1);
            border-radius: 50%;
            transition: var(--transition);
        }

        .option-text {
            flex: 1;
        }

        .correct {
            background-color: rgba(46, 204, 113, 0.2);
            border-color: var(--correct-color);
            animation: pulse 0.5s ease;
        }

        .correct .option-label {
            background-color: var(--correct-color);
        }

        .incorrect {
            background-color: rgba(231, 76, 60, 0.2);
            border-color: var(--incorrect-color);
            animation: shake 0.5s ease;
        }

        .incorrect .option-label {
            background-color: var(--incorrect-color);
        }

        .result-popup {
            background-color: rgba(0, 0, 0, 0.8);
            padding: 20px;
            border-radius: var(--border-radius);
            margin-top: 20px;
            border-left: 4px solid #4cc9f0;
            display: none;
        }

        .result-popup.show {
            display: block;
            animation: fadeIn 0.5s ease;
        }

        .result-title {
            font-weight: bold;
            margin-bottom: 10px;
            color: #4cc9f0;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .result-content {
            line-height: 1.7;
        }

        .correct-answer {
            color: var(--correct-color);
            font-weight: bold;
            margin-top: 10px;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .navigation {
            display: flex;
            justify-content: space-between;
            margin-top: 30px;
        }

        .btn {
            padding: 12px 25px;
            background: linear-gradient(135deg, #4cc9f0, #4361ee);
            color: white;
            border: none;
            border-radius: var(--border-radius);
            cursor: pointer;
            font-size: 1rem;
            font-weight: bold;
            transition: var(--transition);
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(76, 201, 240, 0.4);
        }

        .btn:disabled {
            background: #555;
            cursor: not-allowed;
            transform: none;
            box-shadow: none;
        }

        .btn-prev {
            background: linear-gradient(135deg, #f0a04b, #e67e22);
        }

        .btn-finish {
            background: linear-gradient(135deg, #2ecc71, #27ae60);
        }

        .footer {
            text-align: center;
            margin-top: 40px;
            padding: 20px;
            color: #b0b0b0;
            font-size: 0.9rem;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.02); }
            100% { transform: scale(1); }
        }

        @keyframes shake {
            0% { transform: translateX(0); }
            25% { transform: translateX(-5px); }
            50% { transform: translateX(5px); }
            75% { transform: translateX(-5px); }
            100% { transform: translateX(0); }
        }

        /* تصميم متجاوب */
        @media (max-width: 768px) {
            .exam-info {
                flex-direction: column;
            }
            
            .question-container {
                padding: 15px;
            }
            
            .navigation {
                flex-direction: column;
                gap: 15px;
            }
            
            .btn {
                width: 100%;
                justify-content: center;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>محاكي اختبار الرخصة المهنية للمعلمين</h1>
            <p class="subtitle">تم اعداد هذا الاختبار من قبل المعلم : فهد الخالدي</p>
        </header>

        <div class="exam-info">
            <div class="info-item">
                <i>⏱️</i>
                <span>الوقت المتبقي: <span id="timer">02:00:00</span></span>
            </div>
            <div class="info-item">
                <i>❓</i>
                <span>عدد الأسئلة: 68 سؤال</span>
            </div>
            <div class="info-item">
                <i>📊</i>
                <span>المستوى: متقدم</span>
            </div>
        </div>

        <div class="progress-container">
            <div class="progress-bar">
                <div class="progress" id="progress-bar"></div>
            </div>
            <div class="progress-text">
                <span>التقدم: <span id="progress-text">0%</span></span>
                <span>سؤال <span id="current-question">1</span> من 68</span>
            </div>
        </div>

        <div class="question-container">
            <div class="question-header">
                <div class="question-number">سؤال رقم <span id="question-number">1</span></div>
                <div class="question-category" id="question-category">القيم والمسؤوليات المهنية</div>
            </div>

            <div class="question-text" id="question-text">
                <!-- سيتم تعبئة نص السؤال هنا -->
            </div>

            <div class="options-container" id="options-container">
                <!-- سيتم تعبئة الخيارات هنا -->
            </div>

            <div class="result-popup" id="result-popup">
                <div class="result-title">
                    <span>شرح الإجابة</span>
                </div>
                <div class="result-content" id="result-content">
                    <!-- سيتم تعبئة شرح الإجابة هنا -->
                </div>
                <div class="correct-answer" id="correct-answer">
                    <!-- سيتم عرض الإجابة الصحيحة هنا -->
                </div>
            </div>

            <div class="navigation">
                <button class="btn btn-prev" id="prev-btn" disabled>
                    <span>السابق</span>
                </button>
                <button class="btn btn-next" id="next-btn">
                    <span>التالي</span>
                </button>
                <button class="btn btn-finish" id="finish-btn" style="display: none;">
                    <span>إنهاء الاختبار</span>
                </button>
            </div>
        </div>

        <div class="footer">
            <p>جميع الحقوق محفوظة ©  - </p>
        </div>
    </div>

    <!-- عناصر الصوت -->
    <audio id="correct-sound" preload="auto">
        <source src="https://assets.mixkit.co/sfx/preview/mixkit-correct-answer-tone-2870.mp3" type="audio/mpeg">
    </audio>
    <audio id="incorrect-sound" preload="auto">
        <source src="https://assets.mixkit.co/sfx/preview/mixkit-wrong-answer-fail-notification-946.mp3" type="audio/mpeg">
    </audio>

    <script>
        // دالة لإنشاء أسئلة عشوائية مع توزيع متساوٍ للإجابات الصحيحة
        function generateQuestions() {
            const questions = [];
            const categories = [
                "القيم والمسؤوليات المهنية", 
                "المعرفة المهنية", 
                "الممارسات المهنية",
                "التفاعل المهني",
                "التطوير المهني المستمر",
                "تهيئة بيئات التعلم"
            ];
            
            // توزيع عشوائي للإجابات الصحيحة
            const correctAnswers = [];
            for (let i = 0; i < 68; i++) {
                correctAnswers.push(Math.floor(Math.random() * 4));
            }
            
            // إنشاء 68 سؤالاً
            for (let i = 0; i < 68; i++) {
                const category = categories[Math.floor(Math.random() * categories.length)];
                
                questions.push({
                    id: i + 1,
                    category: category,
                    text: generateQuestionText(category),
                    options: generateOptions(category),
                    correctAnswer: correctAnswers[i],
                    explanation: generateExplanation(category)
                });
            }
            
            return questions;
        }
        
        // دالة لإنشاء نص السؤال بناءً على الفئة
        function generateQuestionText(category) {
            const texts = {
                "القيم والمسؤوليات المهنية": [
                    "أي من الممارسات التالية تعكس بشكل أفضل الالتزام بالقيم الإسلامية الوسطية في البيئة التعليمية؟",
                    "ما هي الاستراتيجية الأكثر فعالية لتعزيز الهوية الوطنية لدى الطلاب في سياق تعليمي متعدد الثقافات؟",
                    "كيف يمكن للمعلم تحقيق التوازن بين الالتزام بالقيم الإسلامية والانفتاح على التنوع الثقافي؟",
                    "ما هو الدور الأساسي للمعلم في ترسيخ القيم الأخلاقية في الممارسة التعليمية اليومية؟"
                ],
                "المعرفة المهنية": [
                    "أي من الاستراتيجيات التالية تعزز بشكل أفضل استيعاب النص المسموع والمقروء لدى الطلاب؟",
                    "ما هي الطريقة المثلى لتنمية المهارات اللغوية والكمية في سياق تعليمي متكامل؟",
                    "كيف يمكن للمعلم تطوير مهارات التعبير الكتابي مع مراعاة الكتابة الإملائية السليمة؟",
                    "ما هي الاستراتيجية الأكثر فعالية لتعزيز مهارات القراءة والتحليل النقدي للنصوص؟"
                ],
                "الممارسات المهنية": [
                    "أي من الممارسات التالية تمثل أفضل نموذج للتخطيط للتدريس وتنفيذه؟",
                    "ما هي الاستراتيجية الأكثر فعالية لتهيئة بيئات تعلم تفاعلية وداعمة للمتعلم؟",
                    "كيف يمكن للمعلم تصميم أنشطة تعلم تراعي الفروق الفردية بين الطلاب؟",
                    "ما هو النهج الأمثل لقيادة الأنشطة الصفية بفاعلية وتحقيق أهداف التعلم؟"
                ],
                "التفاعل المهني": [
                    "أي من الممارسات التالية تعزز بشكل أفضل التفاعل مع مجتمعات التعلم المهني؟",
                    "ما هي الاستراتيجية الأكثر فعالية للتفاعل مع أولياء الأمور لتحسين نواتج التعلم؟",
                    "كيف يمكن للمعلم بناء شراكات فعالة مع المجتمع المحلي لتعزيز العملية التعليمية؟",
                    "ما هو الدور الأساسي للمعلم في تعزيز ثقافة التعلم التعاوني بين الزملاء؟"
                ],
                "التطوير المهني المستمر": [
                    "أي من الاستراتيجيات التالية تمثل النهج الأمثل للتطوير المهني المستمر للمعلم؟",
                    "ما هي الطريقة المثلى لوضع خطة تطوير الأداء المهني في ضوء المعايير المهنية؟",
                    "كيف يمكن للمعلم تقييم أثر التطوير المهني على ممارساته التعليمية؟",
                    "ما هو النهج الأكثر فعالية للاستفادة من نتائج التقويم في تطوير الأداء المهني؟"
                ],
                "تهيئة بيئات التعلم": [
                    "أي من الممارسات التالية تسهم بشكل أفضل في تهيئة بيئات تعلم آمنة وجاذبة؟",
                    "ما هي الاستراتيجية الأكثر فعالية لبناء ثقافة تواصل معززة للتعلم؟",
                    "كيف يمكن للمعلم تصميم بيئات تعلم تراعي احتياجات الطلاب ذوي الاحتياجات الخاصة؟",
                    "ما هو النهج الأمثل لتهيئة بيئات تعلم تدعم الإبداع والابتكار؟"
                ]
            };
            
            const categoryTexts = texts[category];
            return categoryTexts[Math.floor(Math.random() * categoryTexts.length)];
        }
        
        // دالة لإنشاء خيارات متشابهة ومربكة
        function generateOptions(category) {
            const options = {
                "القيم والمسؤوليات المهنية": [
                    "تعزيز القيم الإسلامية من خلال الممارسات اليومية مع مراعاة التنوع الثقافي",
                    "التركيز على القيم الإسلامية مع الاهتمام بالهوية الوطنية والانفتاح الثقافي",
                    "تبني منهج متوازن يجمع بين القيم الإسلامية والتفاعل الإيجابي مع الثقافات",
                    "تطوير بيئة تعليمية ترسخ القيم الإسلامية مع احترام التعددية الثقافية"
                ],
                "المعرفة المهنية": [
                    "استخدام استراتيجيات متكاملة تجمع بين الجانب النظري والتطبيقي",
                    "تبني منهجية شاملة تربط بين المعرفة والمهارات في سياقات متنوعة",
                    "تطوير أنشطة تعلم تجمع بين الجوانب المعرفية والمهارية والتطبيقية",
                    "اعتماد أساليب تعلم نشط تدمج بين المعرفة النظرية والتطبيق العملي"
                ],
                "الممارسات المهنية": [
                    "تصميم خطط تدريسية مرنة تراعي الاحتياجات المتنوعة للطلاب",
                    "بناء استراتيجيات تعلم تستجيب للفروق الفردية وتنوع أنماط التعلم",
                    "تطوير ممارسات تدريسية تراعي التنوع وتستجيب للاحتياجات التعليمية",
                    "تبني منهجيات تعليمية متكاملة تستوعب الاختلافات بين المتعلمين"
                ],
                "التفاعل المهني": [
                    "بناء شراكات تعاونية مع مختلف الفاعلين في المجتمع التعليمي",
                    "تطوير شبكات دعم مهنية تعزز تبادل الخبرات والممارسات الناجحة",
                    "إنشاء قنوات اتصال فعالة مع جميع مكونات المجتمع التعليمي",
                    "تأسيس تحالفات مهنية تدعم التطوير المستمر للعملية التعليمية"
                ],
                "التطوير المهني المستمر": [
                    "اعتماد منهجية التطوير القائمة على البحث والتأمل في الممارسة",
                    "تبني استراتيجيات تطوير تستند إلى التحليل والتقييم المستمر",
                    "تطوير خطط تحسين تستفيد من نتائج التقويم والتغذية الراجعة",
                    "بناء مسارات تطوير تعتمد على التشخيص الدقيق للاحتياجات"
                ],
                "تهيئة بيئات التعلم": [
                    "تصميم مساحات تعلم تستجيب للاحتياجات النفسية والاجتماعية للطلاب",
                    "تهيئة أجواء تعليمية تدعم النمو الشامل والشعور بالأمان",
                    "بناء بيئات تعلم تراعي الجوانب العاطفية والاجتماعية للمتعلمين",
                    "تطوير فصول دراسية تدعم التعلم النشط والتعبير عن الذات"
                ]
            };
            
            // إرجاع خيارات عشوائية مع خلطها
            const categoryOptions = [...options[category]];
            return shuffleArray(categoryOptions);
        }
        
        // دالة لإنشاء شرح للإجابة
        function generateExplanation(category) {
            const explanations = {
                "القيم والمسؤوليات المهنية": "هذه الإجابة تعكس التوازن الأمثل بين الالتزام بالقيم الإسلامية الأساسية والانفتاح الإيجابي على التنوع الثقافي، مما يخلق بيئة تعليمية متوازنة تحترم الخصوصية الثقافية مع الحفاظ على الهوية الإسلامية.",
                "المعرفة المهنية": "هذا النهج يدمج بشكل متكامل بين الجوانب النظرية والتطبيقية، مما يمكن الطلاب من ربط المعرفة بالواقع وتطبيقها في سياقات حياتية متنوعة، مما يعزز الفهم العميق والاستيعاب الشامل.",
                "الممارسات المهنية": "هذه الاستراتيجية تراعي التنوع في أنماط التعلم والفروق الفردية بين الطلاب، مما يضمن تلبية الاحتياجات التعليمية المتباينة وتحقيق أقصى استفادة ممكنة لجميع المتعلمين.",
                "التفاعل المهني": "هذا النموذج يبني جسوراً فعالة للتواصل والتعاون بين جميع الأطراف المعنية بالعملية التعليمية، مما يعزز تبادل الخبرات ويدعم التطوير المستمر للعملية التعليمية.",
                "التطوير المهني المستمر": "هذا المنهج يعتمد على التحليل الدقيق والتقييم المستمر، مما يمكن المعلم من تحديد احتياجاته التطويرية بدقة وبناء خطط تحسين فعالة قابلة للقياس.",
                "تهيئة بيئات التعلم": "هذا التصمير يراعي الجوانب النفسية والاجتماعية للمتعلمين، مما يخلق بيئة آمنة وداعمة تمكن الطلاب من التعبير عن أنفسهم والمشاركة الفاعلة في عملية التعلم."
            };
            
            return explanations[category];
        }
        
        // دالة لخلط المصفوفة عشوائياً
        function shuffleArray(array) {
            const newArray = [...array];
            for (let i = newArray.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [newArray[i], newArray[j]] = [newArray[j], newArray[i]];
            }
            return newArray;
        }

        // إنشاء الأسئلة
        const questions = generateQuestions();

        // متغيرات التطبيق
        let currentQuestionIndex = 0;
        let userAnswers = new Array(questions.length).fill(null);
        let timerInterval;
        let answerSelected = false;

        // عناصر DOM
        const questionNumberElement = document.getElementById('question-number');
        const questionCategoryElement = document.getElementById('question-category');
        const questionTextElement = document.getElementById('question-text');
        const optionsContainer = document.getElementById('options-container');
        const resultPopup = document.getElementById('result-popup');
        const resultContent = document.getElementById('result-content');
        const correctAnswerElement = document.getElementById('correct-answer');
        const prevBtn = document.getElementById('prev-btn');
        const nextBtn = document.getElementById('next-btn');
        const finishBtn = document.getElementById('finish-btn');
        const progressBar = document.getElementById('progress-bar');
        const progressText = document.getElementById('progress-text');
        const currentQuestionElement = document.getElementById('current-question');
        const timerElement = document.getElementById('timer');
        const correctSound = document.getElementById('correct-sound');
        const incorrectSound = document.getElementById('incorrect-sound');

        // تهيئة المؤقت
        function initializeTimer() {
            let timeLeft = 2 * 60 * 60; // ساعتان بالثواني
            updateTimerDisplay(timeLeft);
            
            timerInterval = setInterval(() => {
                timeLeft--;
                updateTimerDisplay(timeLeft);
                
                if (timeLeft <= 0) {
                    clearInterval(timerInterval);
                    finishExam();
                }
            }, 1000);
        }
        
        function updateTimerDisplay(seconds) {
            const hours = Math.floor(seconds / 3600);
            const minutes = Math.floor((seconds % 3600) / 60);
            const secs = seconds % 60;
            
            timerElement.textContent = `${hours.toString().padStart(2, '0')}:${minutes.toString().padStart(2, '0')}:${secs.toString().padStart(2, '0')}`;
        }

        // عرض السؤال الحالي
        function displayCurrentQuestion() {
            const question = questions[currentQuestionIndex];
            
            questionNumberElement.textContent = question.id;
            questionCategoryElement.textContent = question.category;
            questionTextElement.textContent = question.text;
            
            // تحديث شريط التقدم
            const progress = ((currentQuestionIndex + 1) / questions.length) * 100;
            progressBar.style.width = `${progress}%`;
            progressText.textContent = `${Math.round(progress)}%`;
            currentQuestionElement.textContent = currentQuestionIndex + 1;
            
            // إعادة تعيين النافذة المنبثقة
            resultPopup.classList.remove('show');
            
            // تعبئة الخيارات
            optionsContainer.innerHTML = '';
            const optionLabels = ['أ', 'ب', 'ج', 'د'];
            
            question.options.forEach((option, index) => {
                const optionElement = document.createElement('div');
                optionElement.className = 'option';
                
                // إذا كان المستخدم قد أجاب على هذا السؤال، عرض النتيجة
                if (userAnswers[currentQuestionIndex] !== null) {
                    if (userAnswers[currentQuestionIndex] === index) {
                        if (userAnswers[currentQuestionIndex] === question.correctAnswer) {
                            optionElement.classList.add('correct');
                        } else {
                            optionElement.classList.add('incorrect');
                        }
                    } else if (index === question.correctAnswer) {
                        optionElement.classList.add('correct');
                    }
                    optionElement.classList.add('disabled');
                }
                
                optionElement.innerHTML = `
                    <div class="option-label">${optionLabels[index]}</div>
                    <div class="option-text">${option}</div>
                `;
                
                // إذا لم يتم الإجابة على السؤال بعد، السماح بالاختيار
                if (userAnswers[currentQuestionIndex] === null) {
                    optionElement.addEventListener('click', () => selectOption(index));
                }
                
                optionsContainer.appendChild(optionElement);
            });
            
            // تحديث أزرار التنقل
            prevBtn.disabled = currentQuestionIndex === 0;
            
            if (currentQuestionIndex === questions.length - 1) {
                nextBtn.style.display = 'none';
                finishBtn.style.display = 'flex';
            } else {
                nextBtn.style.display = 'flex';
                finishBtn.style.display = 'none';
            }
            
            // إذا كان المستخدم قد أجاب على السؤال، عرض النتيجة
            if (userAnswers[currentQuestionIndex] !== null) {
                showResult();
            }
        }

        // اختيار خيار
        function selectOption(optionIndex) {
            if (answerSelected) return; // منع اختيار إجابة أخرى
            
            answerSelected = true;
            userAnswers[currentQuestionIndex] = optionIndex;
            const question = questions[currentQuestionIndex];
            
            // تشغيل الصوت المناسب
            if (optionIndex === question.correctAnswer) {
                correctSound.play();
            } else {
                incorrectSound.play();
            }
            
            // تحديث العرض
            displayCurrentQuestion();
            showResult();
            
            // تمكين زر التالي بعد فترة قصيرة
            setTimeout(() => {
                answerSelected = false;
            }, 1000);
        }

        // عرض نتيجة السؤال
        function showResult() {
            const question = questions[currentQuestionIndex];
            const userAnswer = userAnswers[currentQuestionIndex];
            
            if (userAnswer === null) return;
            
            resultContent.textContent = question.explanation;
            
            if (userAnswer === question.correctAnswer) {
                correctAnswerElement.innerHTML = `<span>✅ الإجابة صحيحة</span>`;
            } else {
                correctAnswerElement.innerHTML = `<span>❌ الإجابة الصحيحة: ${question.options[question.correctAnswer]}</span>`;
            }
            
            resultPopup.classList.add('show');
        }

        // التنقل بين الأسئلة
        nextBtn.addEventListener('click', () => {
            if (currentQuestionIndex < questions.length - 1) {
                currentQuestionIndex++;
                displayCurrentQuestion();
            }
        });

        prevBtn.addEventListener('click', () => {
            if (currentQuestionIndex > 0) {
                currentQuestionIndex--;
                displayCurrentQuestion();
            }
        });

        // إنهاء الاختبار
        finishBtn.addEventListener('click', finishExam);

        function finishExam() {
            clearInterval(timerInterval);
            
            // حساب النتيجة
            let score = 0;
            userAnswers.forEach((answer, index) => {
                if (answer === questions[index].correctAnswer) {
                    score++;
                }
            });
            
            const percentage = (score / questions.length) * 100;
            
            // عرض النتيجة النهائية
            alert(`تم إنهاء الاختبار!\n\nنتيجتك: ${score} من ${questions.length}\nالنسبة المئوية: ${percentage.toFixed(2)}%`);
        }

        // بدء التطبيق
        initializeTimer();
        displayCurrentQuestion();
    </script>
</body>
</html>
