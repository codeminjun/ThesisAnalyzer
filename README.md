<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>논문 분석 시스템 개발 계획서</title>
    <style>
      * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
      }

      body {
        font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
        background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
        min-height: 100vh;
        color: #333;
      }

      .container {
        max-width: 1200px;
        margin: 0 auto;
        padding: 20px;
      }

      .header {
        text-align: center;
        background: rgba(255, 255, 255, 0.1);
        backdrop-filter: blur(10px);
        border-radius: 20px;
        padding: 40px 20px;
        margin-bottom: 30px;
        border: 1px solid rgba(255, 255, 255, 0.2);
        animation: slideDown 0.8s ease-out;
      }

      @keyframes slideDown {
        from {
          opacity: 0;
          transform: translateY(-50px);
        }
        to {
          opacity: 1;
          transform: translateY(0);
        }
      }

      .header h1 {
        font-size: 2.5rem;
        color: white;
        text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
        margin-bottom: 10px;
      }

      .header p {
        color: rgba(255, 255, 255, 0.9);
        font-size: 1.2rem;
      }

      .overview {
        background: rgba(255, 255, 255, 0.95);
        border-radius: 15px;
        padding: 30px;
        margin-bottom: 30px;
        box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
        animation: fadeIn 1s ease-out 0.2s both;
      }

      @keyframes fadeIn {
        from {
          opacity: 0;
          transform: translateY(30px);
        }
        to {
          opacity: 1;
          transform: translateY(0);
        }
      }

      .goals-grid {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
        gap: 20px;
        margin: 20px 0;
      }

      .goal-card {
        background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
        color: white;
        padding: 20px;
        border-radius: 15px;
        text-align: center;
        transition: transform 0.3s ease;
      }

      .goal-card:hover {
        transform: translateY(-5px);
      }

      .week-section {
        background: rgba(255, 255, 255, 0.95);
        border-radius: 15px;
        margin-bottom: 30px;
        overflow: hidden;
        box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
        animation: fadeIn 1s ease-out var(--animation-delay, 0.4s) both;
      }

      .week-header {
        background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
        color: white;
        padding: 20px 30px;
        cursor: pointer;
        transition: all 0.3s ease;
        display: flex;
        justify-content: space-between;
        align-items: center;
      }

      .week-header:hover {
        background: linear-gradient(135deg, #43a3f5 0%, #00e8f5 100%);
      }

      .week-header h3 {
        font-size: 1.5rem;
      }

      .week-toggle {
        font-size: 1.5rem;
        transition: transform 0.3s ease;
      }

      .week-content {
        padding: 30px;
        display: none;
      }

      .week-content.active {
        display: block;
        animation: slideDown 0.5s ease-out;
      }

      .day-card {
        background: #f8f9ff;
        border-left: 4px solid #4facfe;
        margin: 15px 0;
        padding: 20px;
        border-radius: 0 10px 10px 0;
        transition: all 0.3s ease;
      }

      .day-card:hover {
        background: #f0f2ff;
        border-left-color: #667eea;
        transform: translateX(5px);
      }

      .day-title {
        font-weight: bold;
        color: #4facfe;
        margin-bottom: 10px;
        font-size: 1.1rem;
      }

      .task-list {
        list-style: none;
      }

      .task-item {
        margin: 8px 0;
        display: flex;
        align-items: center;
        transition: all 0.3s ease;
      }

      .task-checkbox {
        margin-right: 10px;
        transform: scale(1.2);
        cursor: pointer;
      }

      .task-item:hover {
        color: #4facfe;
      }

      .progress-section {
        background: rgba(255, 255, 255, 0.95);
        border-radius: 15px;
        padding: 30px;
        margin-bottom: 30px;
        box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
      }

      .progress-bar {
        background: #e0e7ff;
        height: 20px;
        border-radius: 10px;
        overflow: hidden;
        margin: 10px 0;
      }

      .progress-fill {
        background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
        height: 100%;
        border-radius: 10px;
        transition: width 1s ease-out;
        width: 0%;
      }

      .tech-stack {
        background: rgba(255, 255, 255, 0.95);
        border-radius: 15px;
        padding: 30px;
        margin-bottom: 30px;
        box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
      }

      .tech-grid {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
        gap: 15px;
        margin-top: 20px;
      }

      .tech-item {
        background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
        color: white;
        padding: 15px;
        border-radius: 10px;
        text-align: center;
        transition: transform 0.3s ease;
      }

      .tech-item:hover {
        transform: scale(1.05);
      }

      .code-block {
        background: #1e293b;
        color: #e2e8f0;
        padding: 20px;
        border-radius: 10px;
        margin: 15px 0;
        overflow-x: auto;
        font-family: "Courier New", monospace;
        border-left: 4px solid #4facfe;
      }

      .share-buttons {
        position: fixed;
        top: 50%;
        right: 20px;
        transform: translateY(-50%);
        display: flex;
        flex-direction: column;
        gap: 10px;
        z-index: 1000;
      }

      .share-btn {
        width: 50px;
        height: 50px;
        border-radius: 50%;
        border: none;
        cursor: pointer;
        transition: all 0.3s ease;
        color: white;
        font-size: 1.2rem;
        display: flex;
        align-items: center;
        justify-content: center;
      }

      .share-btn.copy {
        background: linear-gradient(135deg, #43a3f5 0%, #00e8f5 100%);
      }

      .share-btn.download {
        background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
      }

      .share-btn:hover {
        transform: scale(1.1);
      }

      .footer {
        text-align: center;
        color: rgba(255, 255, 255, 0.8);
        padding: 30px;
        font-size: 0.9rem;
      }

      @media (max-width: 768px) {
        .container {
          padding: 10px;
        }

        .header h1 {
          font-size: 2rem;
        }

        .goals-grid {
          grid-template-columns: 1fr;
        }

        .share-buttons {
          position: static;
          flex-direction: row;
          justify-content: center;
          margin: 20px 0;
          transform: none;
        }
      }

      .notification {
        position: fixed;
        top: 20px;
        right: 20px;
        background: rgba(76, 175, 80, 0.9);
        color: white;
        padding: 15px 20px;
        border-radius: 10px;
        display: none;
        z-index: 1001;
        animation: slideIn 0.3s ease-out;
      }

      @keyframes slideIn {
        from {
          transform: translateX(100%);
          opacity: 0;
        }
        to {
          transform: translateX(0);
          opacity: 1;
        }
      }
    </style>
  </head>
  <body>
    <div class="container">
      <!-- Header -->
      <div class="header">
        <h1>📋 논문 분석 시스템 개발 계획서</h1>
        <p>
          한국어 논문의 문장 흐름, 키워드 추출, 논리적 구조를 자동 분석하는
          시스템
        </p>
      </div>

      <!-- Overview -->
      <div class="overview">
        <h2>🎯 프로젝트 개요</h2>
        <div class="goals-grid">
          <div class="goal-card">
            <h4>문장 흐름 분석</h4>
            <p>목표 정확도: 85%+</p>
          </div>
          <div class="goal-card">
            <h4>키워드 추출</h4>
            <p>목표 정밀도: 80%+</p>
          </div>
          <div class="goal-card">
            <h4>논리적 오류 탐지</h4>
            <p>목표 탐지율: 70%+</p>
          </div>
          <div class="goal-card">
            <h4>API 응답시간</h4>
            <p>목표: 3초 이내</p>
          </div>
        </div>
      </div>

      <!-- Progress -->
      <div class="progress-section">
        <h2>📊 전체 진행률</h2>
        <div class="progress-bar">
          <div class="progress-fill" id="overallProgress"></div>
        </div>
        <p id="progressText">0% 완료 (0/4 주차)</p>
      </div>

      <!-- Week 1 -->
      <div class="week-section" style="--animation-delay: 0.4s">
        <div class="week-header" onclick="toggleWeek(1)">
          <h3>✅ 1주차 - 데이터 수집 및 환경 구축</h3>
          <span class="week-toggle" id="toggle1">▼</span>
        </div>
        <div class="week-content" id="week1">
          <div class="day-card">
            <div class="day-title">Day 1-2: 데이터셋 구축</div>
            <ul class="task-list">
              <li class="task-item">
                <input
                  type="checkbox"
                  class="task-checkbox"
                  onchange="updateProgress()"
                />
                <span
                  >논문 샘플 수집 (50편) - 대학 학위논문 20편, 학술지 논문 20편,
                  학회 발표논문 10편</span
                >
              </li>
              <li class="task-item">
                <input
                  type="checkbox"
                  class="task-checkbox"
                  onchange="updateProgress()"
                />
                <span
                  >Ground Truth 데이터 생성 - 전문가 3명이 문장 흐름 평가</span
                >
              </li>
              <li class="task-item">
                <input
                  type="checkbox"
                  class="task-checkbox"
                  onchange="updateProgress()"
                />
                <span>주요 키워드 수동 태깅 (논문당 10-15개)</span>
              </li>
            </ul>
          </div>

          <div class="day-card">
            <div class="day-title">Day 3-4: 기술 스택 세팅</div>
            <ul class="task-list">
              <li class="task-item">
                <input
                  type="checkbox"
                  class="task-checkbox"
                  onchange="updateProgress()"
                />
                <span>한국어 NLP 환경 구축</span>
              </li>
              <li class="task-item">
                <input
                  type="checkbox"
                  class="task-checkbox"
                  onchange="updateProgress()"
                />
                <span>형태소 분석기 성능 테스트 (Okt, Mecab, Hannanum)</span>
              </li>
              <li class="task-item">
                <input
                  type="checkbox"
                  class="task-checkbox"
                  onchange="updateProgress()"
                />
                <span>MongoDB 스키마 설계</span>
              </li>
            </ul>
            <div class="code-block">
              pip install spacy konlpy nltk scikit-learn python -m spacy
              download ko_core_news_sm
            </div>
          </div>

          <div class="day-card">
            <div class="day-title">Day 5-7: 기본 전처리 파이프라인</div>
            <ul class="task-list">
              <li class="task-item">
                <input
                  type="checkbox"
                  class="task-checkbox"
                  onchange="updateProgress()"
                />
                <span>텍스트 정규화 함수 개발</span>
              </li>
              <li class="task-item">
                <input
                  type="checkbox"
                  class="task-checkbox"
                  onchange="updateProgress()"
                />
                <span>문장 분할 알고리즘 구현</span>
              </li>
              <li class="task-item">
                <input
                  type="checkbox"
                  class="task-checkbox"
                  onchange="updateProgress()"
                />
                <span>초기 성능 테스트 수행</span>
              </li>
            </ul>
          </div>
        </div>
      </div>

      <!-- Week 2 -->
      <div class="week-section" style="--animation-delay: 0.6s">
        <div class="week-header" onclick="toggleWeek(2)">
          <h3>✅ 2주차 - 핵심 분석 기능 개발</h3>
          <span class="week-toggle" id="toggle2">▼</span>
        </div>
        <div class="week-content" id="week2">
          <div class="day-card">
            <div class="day-title">Day 8-10: 키워드 추출 시스템</div>
            <ul class="task-list">
              <li class="task-item">
                <input
                  type="checkbox"
                  class="task-checkbox"
                  onchange="updateProgress()"
                />
                <span>TF-IDF 기반 키워드 추출 구현</span>
              </li>
              <li class="task-item">
                <input
                  type="checkbox"
                  class="task-checkbox"
                  onchange="updateProgress()"
                />
                <span>TextRank 알고리즘 구현</span>
              </li>
              <li class="task-item">
                <input
                  type="checkbox"
                  class="task-checkbox"
                  onchange="updateProgress()"
                />
                <span>도메인별 키워드 가중치 시스템 개발</span>
              </li>
              <li class="task-item">
                <input
                  type="checkbox"
                  class="task-checkbox"
                  onchange="updateProgress()"
                />
                <span
                  >키워드 추출 정확도 평가 (Precision, Recall, F1-score)</span
                >
              </li>
            </ul>
          </div>

          <div class="day-card">
            <div class="day-title">Day 11-12: 문장 흐름 분석</div>
            <ul class="task-list">
              <li class="task-item">
                <input
                  type="checkbox"
                  class="task-checkbox"
                  onchange="updateProgress()"
                />
                <span>응집성(Coherence) 측정 구현</span>
              </li>
              <li class="task-item">
                <input
                  type="checkbox"
                  class="task-checkbox"
                  onchange="updateProgress()"
                />
                <span>전환 표현 감지 시스템</span>
              </li>
              <li class="task-item">
                <input
                  type="checkbox"
                  class="task-checkbox"
                  onchange="updateProgress()"
                />
                <span>단락별 주제 일관성 검사</span>
              </li>
            </ul>
          </div>

          <div class="day-card">
            <div class="day-title">Day 13-14: 기본 API 구축</div>
            <ul class="task-list">
              <li class="task-item">
                <input
                  type="checkbox"
                  class="task-checkbox"
                  onchange="updateProgress()"
                />
                <span>FastAPI 서버 구축</span>
              </li>
              <li class="task-item">
                <input
                  type="checkbox"
                  class="task-checkbox"
                  onchange="updateProgress()"
                />
                <span>MongoDB 연동</span>
              </li>
              <li class="task-item">
                <input
                  type="checkbox"
                  class="task-checkbox"
                  onchange="updateProgress()"
                />
                <span>기본 CRUD 작업 구현</span>
              </li>
            </ul>
          </div>
        </div>
      </div>

      <!-- Week 3 -->
      <div class="week-section" style="--animation-delay: 0.8s">
        <div class="week-header" onclick="toggleWeek(3)">
          <h3>✅ 3주차 - 고급 분석 및 논리 검증</h3>
          <span class="week-toggle" id="toggle3">▼</span>
        </div>
        <div class="week-content" id="week3">
          <div class="day-card">
            <div class="day-title">Day 15-17: 논리적 구조 분석</div>
            <ul class="task-list">
              <li class="task-item">
                <input
                  type="checkbox"
                  class="task-checkbox"
                  onchange="updateProgress()"
                />
                <span>논증 구조 파악 (주장-근거-결론)</span>
              </li>
              <li class="task-item">
                <input
                  type="checkbox"
                  class="task-checkbox"
                  onchange="updateProgress()"
                />
                <span>논리적 비약 탐지 알고리즘</span>
              </li>
              <li class="task-item">
                <input
                  type="checkbox"
                  class="task-checkbox"
                  onchange="updateProgress()"
                />
                <span>인용 및 참고문헌 일관성 검사</span>
              </li>
            </ul>
          </div>

          <div class="day-card">
            <div class="day-title">Day 18-19: 섹션별 심화 분석</div>
            <ul class="task-list">
              <li class="task-item">
                <input
                  type="checkbox"
                  class="task-checkbox"
                  onchange="updateProgress()"
                />
                <span>서론 분석 (연구 목적 명확성, 선행연구 검토)</span>
              </li>
              <li class="task-item">
                <input
                  type="checkbox"
                  class="task-checkbox"
                  onchange="updateProgress()"
                />
                <span>본론 분석 (방법론 설명, 결과 제시 논리)</span>
              </li>
              <li class="task-item">
                <input
                  type="checkbox"
                  class="task-checkbox"
                  onchange="updateProgress()"
                />
                <span>결론 분석 (요약 적절성, 한계점 인식)</span>
              </li>
              <li class="task-item">
                <input
                  type="checkbox"
                  class="task-checkbox"
                  onchange="updateProgress()"
                />
                <span>종합 점수화 시스템 개발</span>
              </li>
            </ul>
          </div>

          <div class="day-card">
            <div class="day-title">Day 20-21: 시각화 및 리포트 생성</div>
            <ul class="task-list">
              <li class="task-item">
                <input
                  type="checkbox"
                  class="task-checkbox"
                  onchange="updateProgress()"
                />
                <span>분석 결과 시각화 (워드클라우드, 그래프, 차트)</span>
              </li>
              <li class="task-item">
                <input
                  type="checkbox"
                  class="task-checkbox"
                  onchange="updateProgress()"
                />
                <span>개선 제안 자동 생성 시스템</span>
              </li>
            </ul>
          </div>
        </div>
      </div>

      <!-- Week 4 -->
      <div class="week-section" style="--animation-delay: 1s">
        <div class="week-header" onclick="toggleWeek(4)">
          <h3>✅ 4주차 - 최적화 및 배포 준비</h3>
          <span class="week-toggle" id="toggle4">▼</span>
        </div>
        <div class="week-content" id="week4">
          <div class="day-card">
            <div class="day-title">Day 22-24: 성능 최적화</div>
            <ul class="task-list">
              <li class="task-item">
                <input
                  type="checkbox"
                  class="task-checkbox"
                  onchange="updateProgress()"
                />
                <span>분석 속도 개선 (멀티프로세싱, 캐싱)</span>
              </li>
              <li class="task-item">
                <input
                  type="checkbox"
                  class="task-checkbox"
                  onchange="updateProgress()"
                />
                <span>메모리 사용량 최적화</span>
              </li>
              <li class="task-item">
                <input
                  type="checkbox"
                  class="task-checkbox"
                  onchange="updateProgress()"
                />
                <span>API 응답시간 3초 이내 달성</span>
              </li>
            </ul>
          </div>

          <div class="day-card">
            <div class="day-title">Day 25-26: 정확도 향상</div>
            <ul class="task-list">
              <li class="task-item">
                <input
                  type="checkbox"
                  class="task-checkbox"
                  onchange="updateProgress()"
                />
                <span>머신러닝 모델 튜닝</span>
              </li>
              <li class="task-item">
                <input
                  type="checkbox"
                  class="task-checkbox"
                  onchange="updateProgress()"
                />
                <span>앙상블 방법 적용</span>
              </li>
              <li class="task-item">
                <input
                  type="checkbox"
                  class="task-checkbox"
                  onchange="updateProgress()"
                />
                <span>오류 패턴 분석 및 수정</span>
              </li>
            </ul>
          </div>

          <div class="day-card">
            <div class="day-title">Day 27-28: 사용자 피드백 시스템</div>
            <ul class="task-list">
              <li class="task-item">
                <input
                  type="checkbox"
                  class="task-checkbox"
                  onchange="updateProgress()"
                />
                <span>A/B 테스트 환경 구축</span>
              </li>
              <li class="task-item">
                <input
                  type="checkbox"
                  class="task-checkbox"
                  onchange="updateProgress()"
                />
                <span>사용자 만족도 조사 시스템</span>
              </li>
              <li class="task-item">
                <input
                  type="checkbox"
                  class="task-checkbox"
                  onchange="updateProgress()"
                />
                <span>피드백 수집 및 분석 로직</span>
              </li>
              <li class="task-item">
                <input
                  type="checkbox"
                  class="task-checkbox"
                  onchange="updateProgress()"
                />
                <span>최종 테스트 및 문서화</span>
              </li>
            </ul>
          </div>
        </div>
      </div>

      <!-- Tech Stack -->
      <div class="tech-stack">
        <h2>🛠 기술 스택</h2>
        <div class="tech-grid">
          <div class="tech-item">
            spaCy 3.4.4<br /><small>문장 구조 분석</small>
          </div>
          <div class="tech-item">
            konlpy 0.6.0<br /><small>한국어 형태소 분석</small>
          </div>
          <div class="tech-item">
            scikit-learn 1.1.3<br /><small>머신러닝</small>
          </div>
          <div class="tech-item">
            FastAPI 0.95.0<br /><small>API 서버</small>
          </div>
          <div class="tech-item">MongoDB<br /><small>데이터베이스</small></div>
          <div class="tech-item">
            NumPy & Pandas<br /><small>데이터 처리</small>
          </div>
        </div>
      </div>

      <!-- Footer -->
      <div class="footer">
        <p>
          단국대학교 모바일시스템공학과 Minjun Kim / Nakyung Kim / Jiwoo Noh
        </p>
      </div>
    </div>

    <!-- Share Buttons -->
    <div class="share-buttons">
      <button
        class="share-btn copy"
        onclick="copyToClipboard()"
        title="링크 복사"
      >
        📋
      </button>
      <button
        class="share-btn download"
        onclick="downloadPlan()"
        title="계획서 다운로드"
      >
        💾
      </button>
    </div>

    <!-- Notification -->
    <div class="notification" id="notification">
      링크가 클립보드에 복사되었습니다!
    </div>

    <script>
      function toggleWeek(weekNum) {
        const content = document.getElementById(`week${weekNum}`);
        const toggle = document.getElementById(`toggle${weekNum}`);

        if (content.classList.contains("active")) {
          content.classList.remove("active");
          toggle.textContent = "▼";
        } else {
          content.classList.add("active");
          toggle.textContent = "▲";
        }
      }

      function updateProgress() {
        const totalTasks = document.querySelectorAll(".task-checkbox").length;
        const completedTasks = document.querySelectorAll(
          ".task-checkbox:checked"
        ).length;
        const percentage = Math.round((completedTasks / totalTasks) * 100);

        const progressFill = document.getElementById("overallProgress");
        const progressText = document.getElementById("progressText");

        progressFill.style.width = percentage + "%";
        progressText.textContent = `${percentage}% 완료 (${completedTasks}/${totalTasks} 작업)`;

        // 완료된 주차 계산
        const completedWeeks = Math.floor(completedTasks / (totalTasks / 4));
        if (completedWeeks > 0) {
          progressText.textContent += ` - ${completedWeeks}/4 주차 완료`;
        }
      }

      function copyToClipboard() {
        navigator.clipboard.writeText(window.location.href).then(() => {
          showNotification("링크가 클립보드에 복사되었습니다!");
        });
      }

      function downloadPlan() {
        const element = document.createElement("a");
        const content = document.documentElement.outerHTML;
        const file = new Blob([content], { type: "text/html" });
        element.href = URL.createObjectURL(file);
        element.download = "논문분석시스템_개발계획서.html";
        document.body.appendChild(element);
        element.click();
        document.body.removeChild(element);
        showNotification("계획서가 다운로드되었습니다!");
      }

      function showNotification(message) {
        const notification = document.getElementById("notification");
        notification.textContent = message;
        notification.style.display = "block";

        setTimeout(() => {
          notification.style.display = "none";
        }, 3000);
      }

      // 페이지 로드시 프로그레스 초기화
      document.addEventListener("DOMContentLoaded", function () {
        updateProgress();

        // 애니메이션 순차 실행
        setTimeout(() => {
          document.getElementById("overallProgress").style.width = "0%";
        }, 1000);
      });

      // 체크박스 상태 저장/복원
      document.addEventListener("DOMContentLoaded", function () {
        const checkboxes = document.querySelectorAll(".task-checkbox");

        // 저장된 상태 복원
        checkboxes.forEach((checkbox, index) => {
          const saved = localStorage.getItem(`task_${index}`);
          if (saved === "true") {
            checkbox.checked = true;
          }
        });

        // 상태 변경시 저장
        checkboxes.forEach((checkbox, index) => {
          checkbox.addEventListener("change", function () {
            localStorage.setItem(`task_${index}`, this.checked);
          });
        });

        updateProgress();
      });
    </script>
  </body>
</html>
