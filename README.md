<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vocabulary Game: Italian Words</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #6a93cb 0%, #a4bfef 100%);
            min-height: 100vh;
            padding: 20px;
            color: #2c3e50;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .container {
            max-width: 1000px;
            width: 100%;
            background: white;
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.2);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            padding: 30px;
            text-align: center;
            position: relative;
        }

        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            position: relative;
            z-index: 1;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
        }

        .header p {
            font-size: 1.2em;
            opacity: 0.9;
            position: relative;
            z-index: 1;
        }

        .nav-buttons {
            display: flex;
            justify-content: center;
            gap: 10px;
            padding: 20px;
            background: #f8f9fa;
            flex-wrap: wrap;
        }

        .nav-btn {
            padding: 12px 24px;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
        }

        .nav-btn.active {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(74, 111, 165, 0.4);
        }

        .nav-btn:not(.active) {
            background: white;
            color: #666;
        }

        .nav-btn:hover:not(.active) {
            background: #e9ecef;
            transform: translateY(-1px);
        }

        .game-section {
            display: none;
            padding: 30px;
            min-height: 400px;
        }

        .game-section.active {
            display: block;
            animation: fadeIn 0.5s ease-in;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .word-bank {
            background: linear-gradient(135deg, #f5f7fa, #e8f4f2);
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 25px;
            border: 2px solid #4a6fa5;
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.2);
        }

        .word-bank h3 {
            color: #4a6fa5;
            margin-bottom: 15px;
            text-align: center;
            font-size: 1.4em;
        }

        .word-options {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            justify-content: center;
        }

        .word-option {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            padding: 10px 18px;
            border-radius: 20px;
            font-weight: bold;
            font-size: 16px;
            box-shadow: 0 3px 10px rgba(74, 111, 165, 0.3);
            transition: all 0.3s ease;
            cursor: default;
        }

        .word-option:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(74, 111, 165, 0.4);
        }

        .question {
            background: #f8f9fa;
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 20px;
            border-left: 5px solid #4a6fa5;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
        }

        .question h3 {
            color: #4a6fa5;
            margin-bottom: 15px;
            font-size: 1.3em;
        }

        .fill-blank {
            background: #fff;
            border: 2px solid #ddd;
            border-radius: 8px;
            padding: 8px 12px;
            font-size: 16px;
            margin: 0 5px;
            min-width: 120px;
            transition: border-color 0.3s ease;
        }

        .fill-blank.correct {
            border-color: #4CAF50;
            background: #e8f5e8;
        }

        .fill-blank.incorrect {
            border-color: #f44336;
            background: #ffeaea;
        }

        .options {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-top: 15px;
        }

        .option {
            padding: 15px 20px;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
        }

        .option:hover {
            border-color: #4a6fa5;
            transform: translateY(-2px);
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.2);
        }

        .option.selected {
            background: #4a6fa5;
            color: white;
            border-color: #4a6fa5;
        }

        .option.correct {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
        }

        .option.incorrect {
            background: #f44336;
            color: white;
            border-color: #f44336;
        }

        .matching-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-top: 20px;
        }

        .match-column h4 {
            text-align: center;
            margin-bottom: 15px;
            color: #4a6fa5;
            font-size: 1.2em;
        }

        .match-item {
            padding: 15px;
            margin: 8px 0;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
        }

        .match-item:hover {
            border-color: #4a6fa5;
            transform: translateY(-1px);
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.2);
        }

        .match-item.selected {
            background: #e8f4f2;
            border-color: #4a6fa5;
        }

        .match-item.matched {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
            cursor: default;
        }

        .check-btn {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            margin: 20px auto;
            display: block;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.3);
        }

        .check-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(74, 111, 165, 0.4);
        }

        .reset-btn {
            background: linear-gradient(135deg, #f44336, #ff7961);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            margin: 10px auto;
            display: block;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(244, 67, 54, 0.3);
        }

        .reset-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(244, 67, 54, 0.4);
        }

        .feedback {
            margin-top: 15px;
            padding: 15px;
            border-radius: 10px;
            font-weight: bold;
            text-align: center;
            animation: slideIn 0.3s ease;
        }

        @keyframes slideIn {
            from { transform: translateX(-20px); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        .feedback.correct {
            background: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }

        .feedback.incorrect {
            background: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }

        .score {
            position: fixed;
            top: 20px;
            right: 20px;
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            padding: 15px 20px;
            border-radius: 25px;
            font-weight: bold;
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.3);
            z-index: 1000;
        }

        .icon {
            font-size: 24px;
            margin-right: 10px;
            vertical-align: middle;
        }

        /* Vocabulary List Styles */
        .vocabulary-list {
            padding: 20px;
        }

        .vocabulary-item {
            margin-bottom: 25px;
            padding: 20px;
            border-radius: 10px;
            background: #f8f9fa;
            box-shadow: 0 4px 10px rgba(0,0,0,0.05);
        }

        .vocabulary-item h3 {
            color: #4a6fa5;
            margin-bottom: 10px;
            font-size: 1.4em;
            border-bottom: 2px solid #4a6fa5;
            padding-bottom: 8px;
        }

        .vocabulary-item p {
            margin-bottom: 8px;
            line-height: 1.6;
        }

        .example {
            font-style: italic;
            color: #555;
            padding-left: 15px;
            border-left: 3px solid #4a6fa5;
            margin-top: 10px;
        }

        .italian-flag {
            display: inline-block;
            width: 20px;
            height: 15px;
            background: linear-gradient(to right, #009246 33%, white 33%, white 66%, #CE2B37 66%);
            margin-right: 8px;
            border-radius: 2px;
            vertical-align: middle;
        }

        @media (max-width: 768px) {
            .matching-container {
                grid-template-columns: 1fr;
                gap: 20px;
            }
            
            .nav-buttons {
                flex-direction: column;
                align-items: center;
            }
            
            .nav-btn {
                width: 200px;
            }
            
            .score {
                position: static;
                margin: 20px auto;
                display: block;
                width: fit-content;
            }
        }
    </style>
</head>
<body>
    <div class="score">Score: <span id="score">0</span>/12</div>
    
    <div class="container">
        <div class="header">
            <h1><i class="fas fa-book icon"></i> Vocabulary Game: Italian Words</h1>
            <p>Test your knowledge of these Italian words!</p>
        </div>

        <div class="nav-buttons">
            <button class="nav-btn active" onclick="showSection('vocabulary')">Vocabulary List</button>
            <button class="nav-btn" onclick="showSection('fill-gaps')">Fill in the Gaps</button>
            <button class="nav-btn" onclick="showSection('matching')">Match Definitions</button>
            <button class="nav-btn" onclick="showSection('multiple-choice')">Multiple Choice</button>
        </div>

        <!-- Vocabulary List Section -->
        <div id="vocabulary" class="game-section active">
            <h2 style="text-align: center; margin-bottom: 20px; color: #4a6fa5;">Italian Vocabulary</h2>
            
            <div class="vocabulary-list">
                <div class="vocabulary-item">
                    <h3><span class="italian-flag"></span>felice</h3>
                    <p><strong>Definition:</strong> Happy, content, pleased</p>
                    <p><strong>Usage:</strong> Describes a state of happiness or contentment.</p>
                    <p class="example"><strong>Example:</strong> "Sono molto felice di vederti." (I'm very happy to see you.)</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3><span class="italian-flag"></span>mite</h3>
                    <p><strong>Definition:</strong> Mild, gentle, temperate</p>
                    <p><strong>Usage:</strong> Describes weather, personality, or conditions that are not extreme.</p>
                    <p class="example"><strong>Example:</strong> "Il clima è mite in primavera." (The climate is mild in spring.)</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3><span class="italian-flag"></span>scorso/a</h3>
                    <p><strong>Definition:</strong> Last, past (masculine/feminine)</p>
                    <p><strong>Usage:</strong> Refers to the previous occurrence of something.</p>
                    <p class="example"><strong>Example:</strong> "La settimana scorsa sono andato al cinema." (Last week I went to the cinema.)</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3><span class="italian-flag"></span>incontrare</h3>
                    <p><strong>Definition:</strong> To meet, to encounter</p>
                    <p><strong>Usage:</strong> Used for meeting people or encountering situations.</p>
                    <p class="example"><strong>Example:</strong> "Ho incontrato Maria per strada." (I met Maria on the street.)</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3><span class="italian-flag"></span>migliore</h3>
                    <p><strong>Definition:</strong> Better, best</p>
                    <p><strong>Usage:</strong> Comparative and superlative form of "buono" (good).</p>
                    <p class="example"><strong>Example:</strong> "Questo è il miglior ristorante della città." (This is the best restaurant in the city.)</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3><span class="italian-flag"></span>genitori</h3>
                    <p><strong>Definition:</strong> Parents</p>
                    <p><strong>Usage:</strong> Refers to one's mother and father.</p>
                    <p class="example"><strong>Example:</strong> "I miei genitori vivono a Roma." (My parents live in Rome.)</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3><span class="italian-flag"></span>quando</h3>
                    <p><strong>Definition:</strong> When</p>
                    <p><strong>Usage:</strong> Used to ask about or refer to time.</p>
                    <p class="example"><strong>Example:</strong> "Quando parti per le vacanze?" (When are you leaving for vacation?)</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3><span class="italian-flag"></span>entrambi</h3>
                    <p><strong>Definition:</strong> Both</p>
                    <p><strong>Usage:</strong> Refers to two people or things together.</p>
                    <p class="example"><strong>Example:</strong> "Entrambi i ragazzi sono italiani." (Both boys are Italian.)</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3><span class="italian-flag"></span>stessa</h3>
                    <p><strong>Definition:</strong> Same (feminine)</p>
                    <p><strong>Usage:</strong> Indicates identity or similarity (feminine form).</p>
                    <p class="example"><strong>Example:</strong> "Abbiamo la stessa macchina." (We have the same car.)</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3><span class="italian-flag"></span>alcune volte</h3>
                    <p><strong>Definition:</strong> Sometimes, a few times</p>
                    <p><strong>Usage:</strong> Indicates occasional occurrence.</p>
                    <p class="example"><strong>Example:</strong> "Alcune volte vado a correre al parco." (Sometimes I go running in the park.)</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3><span class="italian-flag"></span>zona</h3>
                    <p><strong>Definition:</strong> Area, zone</p>
                    <p><strong>Usage:</strong> Refers to a specific geographical area or district.</p>
                    <p class="example"><strong>Example:</strong> "Abito in una zona tranquilla della città." (I live in a quiet area of the city.)</p>
                </div>
            </div>
        </div>

        <!-- Fill in the Gaps Section -->
        <div id="fill-gaps" class="game-section">
            <div class="word-bank">
                <h3><i class="fas fa-list-ul icon"></i> Word Bank - Choose from these words:</h3>
                <div class="word-options">
                    <span class="word-option">felice</span>
                    <span class="word-option">mite</span>
                    <span class="word-option">scorsa</span>
                    <span class="word-option">incontrare</span>
                    <span class="word-option">migliore</span>
                    <span class="word-option">genitori</span>
                    <span class="word-option">quando</span>
                    <span class="word-option">entrambi</span>
                    <span class="word-option">stessa</span>
                    <span class="word-option">alcune volte</span>
                    <span class="word-option">zona</span>
                </div>
            </div>

            <div id="fill-gaps-container">
                <!-- Sentences will be dynamically inserted here -->
            </div>

            <button class="check-btn" onclick="checkFillBlanks()">Check Answers</button>
            <button class="reset-btn" onclick="resetFillBlanks()">Reset Answers</button>
        </div>

        <!-- Matching Section -->
        <div id="matching" class="game-section">
            <h2 style="text-align: center; margin-bottom: 20px; color: #4a6fa5;">Match the Italian words with their English definitions</h2>
            <div class="matching-container">
                <div class="match-column">
                    <h4>Italian Words</h4>
                    <div class="match-item" data-word="felice" onclick="selectMatch(this)">felice</div>
                    <div class="match-item" data-word="mite" onclick="selectMatch(this)">mite</div>
                    <div class="match-item" data-word="scorso/a" onclick="selectMatch(this)">scorso/a</div>
                    <div class="match-item" data-word="incontrare" onclick="selectMatch(this)">incontrare</div>
                    <div class="match-item" data-word="migliore" onclick="selectMatch(this)">migliore</div>
                    <div class="match-item" data-word="genitori" onclick="selectMatch(this)">genitori</div>
                    <div class="match-item" data-word="quando" onclick="selectMatch(this)">quando</div>
                    <div class="match-item" data-word="entrambi" onclick="selectMatch(this)">entrambi</div>
                    <div class="match-item" data-word="stessa" onclick="selectMatch(this)">stessa</div>
                    <div class="match-item" data-word="alcune volte" onclick="selectMatch(this)">alcune volte</div>
                    <div class="match-item" data-word="zona" onclick="selectMatch(this)">zona</div>
                </div>
                <div class="match-column">
                    <h4>English Definitions</h4>
                    <div id="meanings-container">
                        <!-- Meanings will be dynamically inserted here -->
                    </div>
                </div>
            </div>
            <div class="feedback" id="matching-feedback" style="display: none;"></div>
            <button class="check-btn" onclick="checkMatching()">Check Matching</button>
            <button class="reset-btn" onclick="resetMatching()">Reset Matching</button>
        </div>

        <!-- Multiple Choice Section -->
        <div id="multiple-choice" class="game-section">
            <div class="question">
                <h3>Question 1: What does "felice" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Sad</div>
                    <div class="option" onclick="selectOption(this, true)">Happy</div>
                    <div class="option" onclick="selectOption(this, false)">Angry</div>
                    <div class="option" onclick="selectOption(this, false)">Tired</div>
                </div>
                <div class="feedback" id="mc-feedback-1" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 2: What does "mite" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Extreme</div>
                    <div class="option" onclick="selectOption(this, true)">Mild</div>
                    <div class="option" onclick="selectOption(this, false)">Cold</div>
                    <div class="option" onclick="selectOption(this, false)">Hot</div>
                </div>
                <div class="feedback" id="mc-feedback-2" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 3: What does "scorso/a" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Next</div>
                    <div class="option" onclick="selectOption(this, true)">Last</div>
                    <div class="option" onclick="selectOption(this, false)">Current</div>
                    <div class="option" onclick="selectOption(this, false)">Future</div>
                </div>
                <div class="feedback" id="mc-feedback-3" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 4: What does "incontrare" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To avoid</div>
                    <div class="option" onclick="selectOption(this, true)">To meet</div>
                    <div class="option" onclick="selectOption(this, false)">To call</div>
                    <div class="option" onclick="selectOption(this, false)">To leave</div>
                </div>
                <div class="feedback" id="mc-feedback-4" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 5: What does "migliore" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Worse</div>
                    <div class="option" onclick="selectOption(this, true)">Better/Best</div>
                    <div class="option" onclick="selectOption(this, false)">Equal</div>
                    <div class="option" onclick="selectOption(this, false)">Different</div>
                </div>
                <div class="feedback" id="mc-feedback-5" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 6: What does "genitori" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Children</div>
                    <div class="option" onclick="selectOption(this, true)">Parents</div>
                    <div class="option" onclick="selectOption(this, false)">Friends</div>
                    <div class="option" onclick="selectOption(this, false)">Siblings</div>
                </div>
                <div class="feedback" id="mc-feedback-6" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 7: What does "quando" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Where</div>
                    <div class="option" onclick="selectOption(this, true)">When</div>
                    <div class="option" onclick="selectOption(this, false)">Why</div>
                    <div class="option" onclick="selectOption(this, false)">How</div>
                </div>
                <div class="feedback" id="mc-feedback-7" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 8: What does "entrambi" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Neither</div>
                    <div class="option" onclick="selectOption(this, true)">Both</div>
                    <div class="option" onclick="selectOption(this, false)">Only one</div>
                    <div class="option" onclick="selectOption(this, false)">All</div>
                </div>
                <div class="feedback" id="mc-feedback-8" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 9: What does "stessa" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Different</div>
                    <div class="option" onclick="selectOption(this, true)">Same</div>
                    <div class="option" onclick="selectOption(this, false)">Better</div>
                    <div class="option" onclick="selectOption(this, false)">Worse</div>
                </div>
                <div class="feedback" id="mc-feedback-9" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 10: What does "alcune volte" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Always</div>
                    <div class="option" onclick="selectOption(this, true)">Sometimes</div>
                    <div class="option" onclick="selectOption(this, false)">Never</div>
                    <div class="option" onclick="selectOption(this, false)">Often</div>
                </div>
                <div class="feedback" id="mc-feedback-10" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 11: What does "zona" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Time</div>
                    <div class="option" onclick="selectOption(this, true)">Area/Zone</div>
                    <div class="option" onclick="selectOption(this, false)">Person</div>
                    <div class="option" onclick="selectOption(this, false)">Thing</div>
                </div>
                <div class="feedback" id="mc-feedback-11" style="display: none;"></div>
            </div>
            
            <button class="reset-btn" onclick="resetMultipleChoice()">Reset Answers</button>
        </div>
    </div>

    <script>
        let score = 0;
        let selectedWord = null;
        let selectedMeaning = null;
        let matchedPairs = [];
        
        // Track correct answers for each section
        let fillBlanksCorrect = 0;
        let matchingCorrect = 0;
        let multipleChoiceCorrect = 0;
        
        // Definitions for the matching game
        const definitions = [
            { meaning: "felice", text: "Happy" },
            { meaning: "mite", text: "Mild, gentle" },
            { meaning: "scorso/a", text: "Last, past" },
            { meaning: "incontrare", text: "To meet, to encounter" },
            { meaning: "migliore", text: "Better, best" },
            { meaning: "genitori", text: "Parents" },
            { meaning: "quando", text: "When" },
            { meaning: "entrambi", text: "Both" },
            { meaning: "stessa", text: "Same (feminine)" },
            { meaning: "alcune volte", text: "Sometimes, a few times" },
            { meaning: "zona", text: "Area, zone" }
        ];

        // Sentences for the fill-in-the-blanks game
        const sentences = [
            { text: "Sono molto <input type='text' class='fill-blank' data-answer='felice' placeholder='answer'> di vederti.", answer: "felice" },
            { text: "Il clima è <input type='text' class='fill-blank' data-answer='mite' placeholder='answer'> in primavera.", answer: "mite" },
            { text: "La settimana <input type='text' class='fill-blank' data-answer='scorsa' placeholder='answer'> sono andato al cinema.", answer: "scorsa" },
            { text: "Ho <input type='text' class='fill-blank' data-answer='incontrato' placeholder='answer'> Maria per strada.", answer: "incontrato" },
            { text: "Questo è il <input type='text' class='fill-blank' data-answer='migliore' placeholder='answer'> ristorante della città.", answer: "migliore" },
            { text: "I miei <input type='text' class='fill-blank' data-answer='genitori' placeholder='answer'> vivono a Roma.", answer: "genitori" },
            { text: "<input type='text' class='fill-blank' data-answer='Quando' placeholder='answer'> parti per le vacanze?", answer: "Quando" },
            { text: "<input type='text' class='fill-blank' data-answer='Entrambi' placeholder='answer'> i ragazzi sono italiani.", answer: "Entrambi" },
            { text: "Abbiamo la <input type='text' class='fill-blank' data-answer='stessa' placeholder='answer'> macchina.", answer: "stessa" },
            { text: "<input type='text' class='fill-blank' data-answer='Alcune volte' placeholder='answer'> vado a correre al parco.", answer: "Alcune volte" },
            { text: "Abito in una <input type='text' class='fill-blank' data-answer='zona' placeholder='answer'> tranquilla della città.", answer: "zona" },
            { text: "Sono <input type='text' class='fill-blank' data-answer='felice' placeholder='answer'> perché ho superato l'esame.", answer: "felice" }
        ];

        // Function to shuffle array (Fisher-Yates algorithm)
        function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
            return array;
        }

        // Initialize the fill-in-the-blanks game with shuffled sentences
        function initFillBlanks() {
            const container = document.getElementById('fill-gaps-container');
            container.innerHTML = '';
            
            // Shuffle the sentences
            const shuffledSentences = shuffleArray([...sentences]);
            
            // Create and append the sentence elements
            shuffledSentences.forEach((sentence, index) => {
                const div = document.createElement('div');
                div.className = 'question';
                div.innerHTML = `
                    <h3>Question ${index + 1}:</h3>
                    <p>${sentence.text}</p>
                    <div class="feedback" id="feedback-${index + 1}" style="display: none;"></div>
                `;
                container.appendChild(div);
            });
        }

        // Initialize the matching game with shuffled definitions
        function initMatchingGame() {
            const meaningsContainer = document.getElementById('meanings-container');
            meaningsContainer.innerHTML = '';
            
            // Shuffle the definitions
            const shuffledDefinitions = shuffleArray([...definitions]);
            
            // Create and append the definition elements
            shuffledDefinitions.forEach(def => {
                const div = document.createElement('div');
                div.className = 'match-item';
                div.setAttribute('data-meaning', def.meaning);
                div.onclick = function() { selectMatch(this); };
                div.textContent = def.text;
                meaningsContainer.appendChild(div);
            });
        }

        function showSection(sectionId) {
            // Hide all sections
            document.querySelectorAll('.game-section').forEach(section => {
                section.classList.remove('active');
            });
            
            // Remove active class from all buttons
            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            
            // Show selected section
            document.getElementById(sectionId).classList.add('active');
            
            // Add active class to clicked button
            event.target.classList.add('active');
            
            // If showing fill-in-the-blanks section, reinitialize with shuffled sentences
            if (sectionId === 'fill-gaps') {
                initFillBlanks();
            }
            
            // If showing matching section, reinitialize with shuffled definitions
            if (sectionId === 'matching') {
                initMatchingGame();
                // Reset matching game state
                document.querySelectorAll('.match-item').forEach(item => {
                    item.classList.remove('selected', 'matched');
                });
                selectedWord = null;
                selectedMeaning = null;
                matchedPairs = [];
                document.getElementById('matching-feedback').style.display = 'none';
            }
            
            // Update score display
            updateScore();
        }

        function checkFillBlanks() {
            const blanks = document.querySelectorAll('.fill-blank');
            let correctCount = 0;
            
            blanks.forEach((blank, index) => {
                const userAnswer = blank.value.toLowerCase().trim();
                const correctAnswer = blank.dataset.answer.toLowerCase();
                
                if (userAnswer === correctAnswer) {
                    blank.classList.remove('incorrect');
                    blank.classList.add('correct');
                    correctCount++;
                } else {
                    blank.classList.remove('correct');
                    blank.classList.add('incorrect');
                }
                
                // Show feedback for each question
                const feedback = document.getElementById(`feedback-${index+1}`);
                if (userAnswer === correctAnswer) {
                    feedback.textContent = '✅ Correct!';
                    feedback.className = 'feedback correct';
                } else {
                    feedback.textContent = `❌ Incorrect. The correct answer is: "${blank.dataset.answer}"`;
                    feedback.className = 'feedback incorrect';
                }
                feedback.style.display = 'block';
            });
            
            fillBlanksCorrect = correctCount;
            updateScore();
        }

        function resetFillBlanks() {
            const blanks = document.querySelectorAll('.fill-blank');
            blanks.forEach(blank => {
                blank.value = '';
                blank.classList.remove('correct', 'incorrect');
            });
            
            const feedbacks = document.querySelectorAll('#fill-gaps .feedback');
            feedbacks.forEach(feedback => {
                feedback.style.display = 'none';
            });
            
            fillBlanksCorrect = 0;
            updateScore();
        }

        function selectMatch(element) {
            if (element.classList.contains('matched')) return;
            
            if (element.dataset.word) {
                // Word selected
                if (selectedWord) selectedWord.classList.remove('selected');
                selectedWord = element;
                element.classList.add('selected');
            } else {
                // Meaning selected
                if (selectedMeaning) selectedMeaning.classList.remove('selected');
                selectedMeaning = element;
                element.classList.add('selected');
            }
            
            // Check if we have both word and meaning selected
            if (selectedWord && selectedMeaning) {
                checkMatch();
            }
        }

        function checkMatch() {
            const feedback = document.getElementById('matching-feedback');
            
            if (selectedWord.dataset.word === selectedMeaning.dataset.meaning) {
                // Correct match
                selectedWord.classList.remove('selected');
                selectedWord.classList.add('matched');
                selectedMeaning.classList.remove('selected');
                selectedMeaning.classList.add('matched');
                
                matchedPairs.push(selectedWord.dataset.word);
                
                feedback.textContent = '✅ Correct match!';
                feedback.className = 'feedback correct';
                
                // Check if all matches are complete
                if (matchedPairs.length === definitions.length) {
                    feedback.textContent = '🎉 Congratulations! You matched all terms correctly!';
                }
            } else {
                // Incorrect match
                feedback.textContent = '❌ Incorrect match. Try again.';
                feedback.className = 'feedback incorrect';
            }
            
            feedback.style.display = 'block';
            selectedWord = null;
            selectedMeaning = null;
            
            matchingCorrect = matchedPairs.length;
            updateScore();
        }

        function checkMatching() {
            const allMatches = document.querySelectorAll('.match-item[data-word]');
            let allCorrect = true;
            
            allMatches.forEach(item => {
                if (!item.classList.contains('matched')) {
                    allCorrect = false;
                }
            });
            
            const feedback = document.getElementById('matching-feedback');
            if (allCorrect) {
                feedback.textContent = '🎉 Excellent! All matches are correct!';
                feedback.className = 'feedback correct';
            } else {
                const unmatchedCount = definitions.length - matchedPairs.length;
                feedback.textContent = `You have ${unmatchedCount} unmatched pair${unmatchedCount !== 1 ? 's' : ''}. Keep trying!`;
                feedback.className = 'feedback incorrect';
            }
            feedback.style.display = 'block';
        }

        function resetMatching() {
            document.querySelectorAll('.match-item').forEach(item => {
                item.classList.remove('selected', 'matched');
            });
            
            initMatchingGame();
            
            selectedWord = null;
            selectedMeaning = null;
            matchedPairs = [];
            
            document.getElementById('matching-feedback').style.display = 'none';
            
            matchingCorrect = 0;
            updateScore();
        }

        function selectOption(element, isCorrect) {
            // Remove selection from all options in this question
            const options = element.parentElement.querySelectorAll('.option');
            options.forEach(opt => {
                opt.classList.remove('selected');
                opt.classList.remove('correct');
                opt.classList.remove('incorrect');
            });
            
            // Mark the selected option
            element.classList.add('selected');
            
            const questionNumber = element.closest('.question').querySelector('h3').textContent.match(/\d+/)[0];
            const feedback = document.getElementById(`mc-feedback-${questionNumber}`);
            
            if (isCorrect) {
                element.classList.add('correct');
                feedback.textContent = '✅ Correct!';
                feedback.className = 'feedback correct';
            } else {
                element.classList.add('incorrect');
                feedback.textContent = '❌ Incorrect. Try again.';
                feedback.className = 'feedback incorrect';
                
                // Show the correct answer
                options.forEach(opt => {
                    if (opt.onclick.toString().includes('true')) {
                        opt.classList.add('correct');
                    }
                });
            }
            
            feedback.style.display = 'block';
            
            // Count correct answers in multiple choice
            multipleChoiceCorrect = document.querySelectorAll('#multiple-choice .option.correct.selected').length;
            updateScore();
        }

        function resetMultipleChoice() {
            document.querySelectorAll('#multiple-choice .option').forEach(option => {
                option.classList.remove('selected', 'correct', 'incorrect');
            });
            
            document.querySelectorAll('#multiple-choice .feedback').forEach(feedback => {
                feedback.style.display = 'none';
            });
            
            multipleChoiceCorrect = 0;
            updateScore();
        }

        function updateScore() {
            // Total score
            score = fillBlanksCorrect + matchingCorrect + multipleChoiceCorrect;
            document.getElementById('score').textContent = score;
        }
        
        // Initialize the page
        window.onload = function() {
            initFillBlanks();
            initMatchingGame();
        }
    </script>
</body>
</html>
