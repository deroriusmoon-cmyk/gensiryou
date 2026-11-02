<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>原子量・分子量・式量 マスターゲーム</title>

  <style>
    :root {
      --blue: #1763b1;
      --blue-dark: #0d4b89;
      --text: #17324d;
      --pale: #eef6ff;
      --green: #157347;
      --red: #b42318;
      --border: #ccd9e6;
    }

    * {
      box-sizing: border-box;
    }

    html {
      scroll-behavior: smooth;
    }

    body {
      margin: 0;
      background: #f5f8fc;
      color: var(--text);
      font-family: system-ui, -apple-system, "Hiragino Kaku Gothic ProN",
                   "Yu Gothic", sans-serif;
      line-height: 1.6;
    }

    header {
      background: linear-gradient(120deg, #104b87, #287bc1);
      color: white;
      text-align: center;
      padding: 16px;
    }

    header h1 {
      margin: 0 0 4px;
      font-size: clamp(1.35rem, 3vw, 2rem);
    }

    header p {
      margin: 0;
    }

    main {
      width: min(100%, 1120px);
      margin: 0 auto;
      padding: 16px;
    }

    section {
      background: white;
      border: 1px solid var(--border);
      border-radius: 14px;
      padding: 22px;
      box-shadow: 0 3px 12px #16395b0a;
    }

    [hidden] {
      display: none !important;
    }

    h2 {
      margin: 0 0 12px;
      color: #14528d;
    }

    p {
      margin: 6px 0 12px;
    }

    button {
      min-height: 48px;
      border: 0;
      border-radius: 10px;
      padding: 10px 16px;
      background: var(--blue);
      color: white;
      font: inherit;
      font-weight: 700;
      cursor: pointer;
      touch-action: manipulation;
    }

    button:hover:not(:disabled) {
      background: var(--blue-dark);
    }

    button:focus-visible,
    summary:focus-visible,
    h2:focus-visible {
      outline: 3px solid #f6ba42;
      outline-offset: 3px;
    }

    button:disabled {
      cursor: default;
    }

    button.secondary {
      background: #526d83;
    }

    button.secondary:hover:not(:disabled) {
      background: #3d586d;
    }

    .small {
      color: #526579;
      font-size: 0.93rem;
    }

    /* メニュー */

    .menu-grid {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: 16px;
      margin: 18px 0;
    }

    button.menu-button {
      display: flex;
      align-items: center;
      gap: 16px;
      width: 100%;
      min-height: 125px;
      padding: 18px;
      text-align: left;
      background: var(--pale);
      color: var(--text);
      border: 2px solid #b9d5ee;
      border-radius: 14px;
    }

    button.menu-button:hover:not(:disabled) {
      background: #d9ecfc;
      color: var(--text);
    }

    .menu-icon {
      flex: 0 0 auto;
      font-size: 2.1rem;
      line-height: 1;
    }

    .menu-button strong {
      display: block;
      font-size: 1.08rem;
    }

    .menu-button small {
      display: block;
      margin-top: 4px;
      color: #526579;
      font-size: 0.88rem;
      font-weight: 400;
    }

    /* クイズ画面 */

    .screen-heading {
      display: flex;
      align-items: center;
      justify-content: space-between;
      flex-wrap: wrap;
      gap: 10px;
    }

    .screen-heading h2 {
      margin: 0;
    }

    .stats {
      display: flex;
      flex-wrap: wrap;
      gap: 8px;
      margin: 15px 0;
    }

    .stats span {
      background: var(--pale);
      padding: 5px 12px;
      border-radius: 20px;
      font-weight: 700;
    }

    #question {
      margin: 18px 0 15px;
      font-size: clamp(1.12rem, 2vw, 1.35rem);
      font-weight: 700;
    }

    .choices {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: 12px;
      margin: 14px 0;
    }

    button.choice {
      display: flex;
      align-items: center;
      gap: 9px;
      width: 100%;
      min-height: 88px;
      padding: 12px 16px;
      background: #edf6ff;
      color: var(--text);
      border: 2px solid #b8d3ea;
      border-radius: 12px;
      text-align: left;
      font-size: 1.03rem;
    }

    button.choice:hover:not(:disabled) {
      background: #dceeff;
      color: var(--text);
      border-color: var(--blue);
    }

    button.choice:disabled {
      opacity: 1;
    }

    button.choice.correct {
      background: #e4f7e9;
      color: #105b33;
      border-color: var(--green);
    }

    button.choice.wrong {
      background: #ffebe8;
      color: #8e2118;
      border-color: var(--red);
    }

    .choice-letter {
      display: inline-flex;
      flex: 0 0 28px;
      align-items: center;
      justify-content: center;
      width: 28px;
      height: 28px;
      border-radius: 50%;
      background: #c8def2;
      font-size: 0.9rem;
    }

    .choice.correct .choice-letter {
      background: #b4e6c3;
    }

    .choice.wrong .choice-letter {
      background: #f4bcb5;
    }

    .choice-label {
      min-width: 0;
      overflow-x: auto;
      white-space: nowrap;
    }

    /* 分子・分母を上下に並べる分数 */

    .fraction {
      display: inline-flex;
      flex-direction: column;
      align-items: stretch;
      justify-content: center;
      vertical-align: middle;
      text-align: center;
      line-height: 1.15;
      white-space: nowrap;
      margin: 0 0.12em;
      font-size: 0.94em;
    }

    .fraction-top,
    .fraction-bottom {
      display: block;
      padding: 0.08em 0.22em;
    }

    .fraction-top {
      border-bottom: 1.7px solid currentColor;
    }

    #feedback {
      padding: 13px 15px;
      margin: 14px 0;
      border-radius: 10px;
      overflow-x: auto;
    }

    #feedback:empty {
      display: none;
    }

    #feedback.correct {
      background: #e8f7ee;
      color: #105b33;
    }

    #feedback.wrong {
      background: #fff0ee;
      color: #8e2118;
    }

    .feedback-answer {
      display: block;
      overflow-x: auto;
      white-space: nowrap;
      font-weight: 700;
    }

    .feedback-explanation {
      display: block;
      margin-top: 6px;
    }

    .game-actions {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
      margin-top: 14px;
    }

    /* 重要ポイントの確認欄 */

    details {
      margin: 12px 0;
      padding: 10px 14px;
      border: 1px solid var(--border);
      border-radius: 10px;
      background: #fbfdff;
    }

    summary {
      cursor: pointer;
      font-weight: 700;
      color: #14528d;
    }

    .reference-grid {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: 10px;
      margin-top: 12px;
    }

    .reference-card {
      padding: 10px;
      background: var(--pale);
      border-left: 4px solid var(--blue);
      border-radius: 6px;
    }

    .reference-card p {
      margin: 3px 0 0;
    }

    /* iPad横向き */

    @media (orientation: landscape) and (min-width: 768px) {
      header {
        padding: 10px 20px;
      }

      header h1 {
        font-size: 1.55rem;
      }

      main {
        padding: 12px 20px;
      }

      section {
        padding: 18px 22px;
      }

      .choices {
        gap: 10px;
      }

      button.choice {
        min-height: 82px;
      }
    }

    /* 狭い画面 */

    @media (max-width: 650px) {
      .menu-grid,
      .choices,
      .reference-grid {
        grid-template-columns: 1fr;
      }

      button.menu-button {
        min-height: 92px;
      }

      button.choice {
        min-height: 70px;
      }

      .screen-heading {
        align-items: stretch;
      }

      .screen-heading h2,
      .screen-heading button,
      .game-actions button {
        width: 100%;
      }
    }
  </style>
</head>

<body>
  <header>
    <h1>⚗️ 原子量・分子量・式量 マスターゲーム</h1>
    <p>高校化学基礎｜4枚のカードから答えを選ぼう</p>
  </header>

  <main>
    <!-- メニュー画面 -->
    <section id="menu" aria-labelledby="menu-title">
      <h2 id="menu-title" tabindex="-1">🏠 メニュー</h2>
      <p>取り組みたい項目を選んでください。</p>

      <div class="menu-grid">
        <button type="button" id="lessonBtn" class="menu-button">
          <span class="menu-icon" aria-hidden="true">📖</span>
          <span>
            <strong>重要ポイントを学ぶ</strong>
            <small>基本事項と計算式を4択クイズで確認</small>
          </span>
        </button>

        <button type="button" id="practiceBtn" class="menu-button">
          <span class="menu-icon" aria-hidden="true">📘</span>
          <span>
            <strong>資料の問題に挑戦</strong>
            <small>ポイントチェック・EXERCISEを4択で解く</small>
          </span>
        </button>

        <button type="button" id="formulaBtn" class="menu-button">
          <span class="menu-icon" aria-hidden="true">🧩</span>
          <span>
            <strong>化学式を選ぶ</strong>
            <small>正しい添字・括弧・電荷を見分ける</small>
          </span>
        </button>

        <button type="button" id="timeBtn" class="menu-button">
          <span class="menu-icon" aria-hidden="true">⏱</span>
          <span>
            <strong>60秒タイムアタック</strong>
            <small>60秒以内にランダムな12問に挑戦</small>
          </span>
        </button>
      </div>

      <p class="small">
        存在比・相対質量・含有率の式では、分数を上下に並べて表示します。
      </p>
    </section>

    <!-- 全モード共通のクイズ画面 -->
    <section id="game" aria-labelledby="game-title" hidden>
      <div class="screen-heading">
        <h2 id="game-title" tabindex="-1">問題に挑戦</h2>

        <button type="button" id="menuBtn" class="secondary">
          ← メニューに戻る
        </button>
      </div>

      <div id="lessonReference" hidden>
        <details>
          <summary>先に重要ポイントを見る／もう一度確認する</summary>

          <div class="reference-grid">
            <div class="reference-card">
              <strong>相対質量</strong>
              <p>
                ¹²C原子1個の質量を12として比較します。
                求めたい原子の質量を¹²C原子の質量で割り、12を掛けます。
              </p>
            </div>

            <div class="reference-card">
              <strong>原子量</strong>
              <p>
                同位体ごとに「相対質量×存在比」を求めて足します。
                99%なら、99を分子、100を分母にした分数を掛けます。
              </p>
            </div>

            <div class="reference-card">
              <strong>分子量</strong>
              <p>
                分子に含まれる各原子について
                「原子量×個数」を足します。
              </p>
            </div>

            <div class="reference-card">
              <strong>式量・含有率</strong>
              <p>
                式量は原子量の合計。
                含有率は「注目する元素の質量÷全体の式量×100」です。
              </p>
            </div>
          </div>
        </details>
      </div>

      <div class="stats">
        <span id="progress">問題：—</span>
        <span id="score">正解：0問</span>
        <span id="timer" hidden>残り：60秒</span>
        <span id="best" hidden>自己ベスト：0問</span>
      </div>

      <div id="question"></div>

      <p id="instruction" class="small">
        正しい答えのカードを1枚選んでください。
      </p>

      <div
        id="choices"
        class="choices"
        role="group"
        aria-label="4択の解答カード"
      ></div>

      <div id="feedback" role="status" aria-live="polite"></div>

      <div class="game-actions">
        <button type="button" id="nextBtn" hidden>
          次の問題へ →
        </button>

        <button type="button" id="restartBtn" class="secondary">
          このモードを最初から
        </button>
      </div>
    </section>
  </main>

  <script>
    "use strict";

    /*
      分数のデータ表記：
        ⟦分子|分母⟧

      例：
        12×⟦99|100⟧＋13×⟦1|100⟧

      画面上では分子・横線・分母の形で表示します。
    */

    const TIME_LIMIT_SECONDS = 60;
    const TIME_QUESTION_COUNT = 12;

    const q = (id, text, answer, wrong, explanation) => ({
      id,
      text,
      answer,
      wrong,
      explanation
    });

    /* 重要ポイント */
    const lessonQuestions = [
      q(
        "基本1",
        "原子の相対質量を決めるとき、基準にする原子は？",
        "¹²C",
        ["¹H", "¹⁶O", "³⁵Cl"],
        "質量数12の炭素原子¹²C 1個の質量を12として比較します。"
      ),

      q(
        "基本2",
        "相対質量について正しい説明は？",
        "比較した値なので単位はない",
        ["単位は g", "単位は mol", "単位は %"],
        "基準と比較した値なので単位はありません。"
      ),

      q(
        "基本3",
        "原子量を求めるときに考慮するものは？",
        "同位体の相対質量と存在比",
        ["陽子の存在比だけ", "原子番号だけ", "電子の速さ"],
        "同位体ごとの相対質量を、存在比に応じて平均します。"
      ),

      q(
        "基本4",
        "相対質量35.0の同位体が75%、37.0の同位体が25%ある。原子量を求める式は？",
        "35.0×⟦75|100⟧＋37.0×⟦25|100⟧",
        [
          "35.0×⟦25|100⟧＋37.0×⟦75|100⟧",
          "(35.0＋37.0)×⟦1|2⟧",
          "35.0×⟦75|100⟧＋37.0×⟦75|100⟧"
        ],
        "相対質量ごとに、その同位体の存在比を掛けて足します。結果は35.5です。"
      ),

      q(
        "基本5",
        "水 H₂O の分子量を求める式は？（原子量：H＝1.0、O＝16）",
        "1.0×2＋16",
        ["1.0＋16", "1.0×16×2", "1.0×2＋16×2"],
        "Hは2個、Oは1個なので、1.0×2＋16です。"
      ),

      q(
        "基本6",
        "NaCl の原子量の合計を表す適切な用語は？",
        "式量",
        ["分子量", "質量数", "原子番号"],
        "NaClは組成式で表すため、原子量の合計を式量といいます。"
      ),

      q(
        "基本7",
        "分子量を用いるのに適切な物質は？",
        "アンモニア NH₃",
        [
          "塩化ナトリウム NaCl",
          "水酸化ナトリウム NaOH",
          "金 Au"
        ],
        "NH₃は分子として表す物質なので、分子量を用います。"
      ),

      q(
        "基本8",
        "イオンの式量を求めるとき、電子の授受による質量変化は？",
        "通常は無視できる",
        ["必ず2倍する", "電荷の数だけ足す", "原子量から10を引く"],
        "電子は原子に比べて非常に軽いため、通常の式量計算では無視します。"
      )
    ];

    /* 添付資料のポイントチェック・EXERCISE・含有率 */
    const practiceQuestions = [
      q(
        "確認(1)",
        "原子量の基準となる元素は？",
        "炭素",
        ["水素", "酸素", "塩素"],
        "質量数12の炭素原子¹²Cを基準にします。"
      ),

      q(
        "確認(2)",
        "基準となる¹²C原子の質量数は？",
        "12",
        ["6", "13", "24"],
        "¹²Cの左肩の12が質量数です。"
      ),

      q(
        "確認(3)",
        "¹²C原子1個の相対質量は？",
        "12",
        ["1", "6", "24"],
        "定義により、¹²C原子1個の相対質量を12とします。"
      ),

      q(
        "確認(4)",
        "¹²C＝12としたとき、¹H原子の相対質量はおよそいくつ？",
        "1.0",
        ["0.1", "12", "16"],
        "¹H原子の相対質量はおよそ1.0です。"
      ),

      q(
        "確認(5)",
        "同じ元素で、質量数の異なる原子を何という？",
        "同位体",
        ["分子", "イオン結晶", "化合物"],
        "陽子数が同じで、中性子数が異なる原子を同位体といいます。"
      ),

      q(
        "確認(6)",
        "同位体の存在比を考慮した相対質量の平均値を何という？",
        "原子量",
        ["分子量", "式量", "質量数"],
        "これが原子量の定義です。"
      ),

      q(
        "確認(7)",
        "¹²Cが99%、¹³Cが1%ある。それぞれの相対質量を12、13とすると、炭素の原子量を求める式は？",
        "12×⟦99|100⟧＋13×⟦1|100⟧",
        [
          "12×⟦1|100⟧＋13×⟦99|100⟧",
          "(12＋13)×⟦1|2⟧",
          "12×⟦99|100⟧＋13×⟦99|100⟧"
        ],
        "12には100分の99、13には100分の1を掛けて足します。結果は12.01です。"
      ),

      q(
        "確認(8)",
        "分子の相対質量を何という？",
        "分子量",
        ["原子番号", "質量数", "存在比"],
        "分子に含まれる原子の原子量を合計して求めます。"
      ),

      q(
        "確認(9)",
        "分子量は、構成する原子の原子量の何を求める？",
        "和",
        ["積", "差", "平均"],
        "「原子量×個数」を元素ごとに求めて足します。"
      ),

      q(
        "確認(10)",
        "水 H₂O の分子量は？（原子量：H＝1.0、O＝16）",
        "18",
        ["17", "32", "34"],
        "1.0×2＋16＝18。"
      ),

      q(
        "確認(11)",
        "組成式やイオンの化学式から求めた原子量の総和は？",
        "式量",
        ["原子番号", "質量数", "存在比"],
        "組成式・イオンの化学式には式量を用います。"
      ),

      q(
        "確認(12)",
        "NaClの式量は？（原子量：Na＝23、Cl＝35.5）",
        "58.5",
        ["35.5", "46.0", "81.5"],
        "23＋35.5＝58.5。"
      ),

      q(
        "確認(13)",
        "イオンの式量で、電子の授受による質量変化は無視できる？",
        "できる",
        ["できない", "陽イオンだけできる", "陰イオンだけできる"],
        "電子は原子に比べて非常に軽いため、通常は無視できます。"
      ),

      q(
        "確認(14)",
        "水酸化物イオン OH⁻ の式量は？（原子量：O＝16、H＝1.0）",
        "17",
        ["15", "16", "18"],
        "16＋1.0＝17。電荷は計算に加えません。"
      ),

      q(
        "確認(15)",
        "分子量を用いるのに適切なのは？",
        "アンモニア",
        ["金", "水酸化ナトリウム", "塩化ナトリウム"],
        "アンモニアNH₃は分子として表す物質です。"
      ),

      q(
        "46",
        "¹²C原子1個が2.0×10⁻²³ g、Al原子1個が4.5×10⁻²³ g。Alの相対質量を求める式は？",
        "⟦4.5×10⁻²³|2.0×10⁻²³⟧×12",
        [
          "⟦2.0×10⁻²³|4.5×10⁻²³⟧×12",
          "⟦4.5×10⁻²³|2.0×10⁻²³⟧",
          "(4.5×10⁻²³)×(2.0×10⁻²³)×12"
        ],
        "Al原子の質量を¹²C原子の質量で割り、基準値12を掛けます。結果は27です。"
      ),

      q(
        "47",
        "¹⁰Bが20.0%、¹¹Bが80.0%。相対質量を10.0、11.0とすると、ホウ素の原子量を求める式は？",
        "10.0×⟦20.0|100⟧＋11.0×⟦80.0|100⟧",
        [
          "10.0×⟦80.0|100⟧＋11.0×⟦20.0|100⟧",
          "(10.0＋11.0)×⟦1|2⟧",
          "10.0×⟦20.0|100⟧＋11.0×⟦20.0|100⟧"
        ],
        "10.0には100分の20.0、11.0には100分の80.0を掛けて足します。結果は10.8です。"
      ),

      q(
        "48(1)",
        "窒素 N₂ の分子量は？（原子量：N＝14）",
        "28",
        ["14", "16", "42"],
        "14×2＝28。"
      ),

      q(
        "48(2)",
        "水 H₂O の分子量は？（原子量：H＝1.0、O＝16）",
        "18",
        ["16", "17", "20"],
        "1.0×2＋16＝18。"
      ),

      q(
        "48(3)",
        "二酸化炭素 CO₂ の分子量は？（原子量：C＝12、O＝16）",
        "44",
        ["28", "32", "60"],
        "12＋16×2＝44。"
      ),

      q(
        "48(4)",
        "硫酸 H₂SO₄ の分子量は？（原子量：H＝1.0、S＝32、O＝16）",
        "98",
        ["82", "96", "114"],
        "1.0×2＋32＋16×4＝98。"
      ),

      q(
        "48(5)",
        "グルコース C₆H₁₂O₆ の分子量は？（原子量：C＝12、H＝1.0、O＝16）",
        "180",
        ["168", "174", "192"],
        "12×6＋1.0×12＋16×6＝180。"
      ),

      q(
        "49(1)",
        "水酸化ナトリウム NaOH の式量は？（原子量：Na＝23、O＝16、H＝1.0）",
        "40",
        ["39", "41", "56"],
        "23＋16＋1.0＝40。"
      ),

      q(
        "49(2)",
        "炭酸カルシウム CaCO₃ の式量は？（原子量：Ca＝40、C＝12、O＝16）",
        "100",
        ["84", "88", "116"],
        "40＋12＋16×3＝100。"
      ),

      q(
        "49(3)",
        "カルシウムイオン Ca²⁺ の式量は？（原子量：Ca＝40）",
        "40",
        ["38", "42", "80"],
        "電子の質量は無視するので、Caの原子量と同じ40です。"
      ),

      q(
        "49(4)",
        "硝酸イオン NO₃⁻ の式量は？（原子量：N＝14、O＝16）",
        "62",
        ["46", "48", "63"],
        "14＋16×3＝62。電荷は加算しません。"
      ),

      q(
        "49(5)",
        "リン酸マグネシウム Mg₃(PO₄)₂ の式量は？（原子量：Mg＝24、P＝31、O＝16）",
        "262",
        ["167", "191", "286"],
        "24×3＋(31＋16×4)×2＝262。括弧の外の2を忘れずに。"
      ),

      q(
        "例題50",
        "Al₂O₃中のAlの含有率を求める式は？（原子量：Al＝27、O＝16）",
        "⟦27×2|27×2＋16×3⟧×100",
        [
          "⟦27|27×2＋16×3⟧×100",
          "⟦16×3|27×2＋16×3⟧×100",
          "⟦27×2＋16×3|27×2⟧×100"
        ],
        "分子はAlの分である27×2、分母はAl₂O₃全体の式量です。結果は52.9%です。"
      ),

      q(
        "50(1)",
        "酸化鉄(Ⅲ) Fe₂O₃ の式量は？（原子量：Fe＝56、O＝16）",
        "160",
        ["112", "144", "176"],
        "56×2＋16×3＝160。"
      ),

      q(
        "50(2)",
        "Fe₂O₃中のFeの含有率を求める式は？（原子量：Fe＝56、O＝16）",
        "⟦56×2|56×2＋16×3⟧×100",
        [
          "⟦56|56×2＋16×3⟧×100",
          "⟦16×3|56×2＋16×3⟧×100",
          "⟦56×2＋16×3|56×2⟧×100"
        ],
        "分子はFeの分である56×2、分母はFe₂O₃全体の式量です。結果は70.0%です。"
      )
    ];

    /* 化学式の4択 */
    const formulaQuestions = [
      q(
        "化学式1",
        "水の化学式は？",
        "H₂O",
        ["HO", "H₂O₂", "HO₂"],
        "水はHが2個、Oが1個です。"
      ),

      q(
        "化学式2",
        "アンモニアの化学式は？",
        "NH₃",
        ["NH₂", "N₂H₃", "NH₄"],
        "アンモニアはNが1個、Hが3個です。"
      ),

      q(
        "化学式3",
        "二酸化炭素の化学式は？",
        "CO₂",
        ["CO", "C₂O", "CO₃"],
        "「二酸化」なので、Oが2個です。"
      ),

      q(
        "化学式4",
        "塩化ナトリウムの組成式は？",
        "NaCl",
        ["Na₂Cl", "NaCl₂", "Na₂Cl₂"],
        "Na⁺とCl⁻の個数比は1：1です。"
      ),

      q(
        "化学式5",
        "水酸化ナトリウムの組成式は？",
        "NaOH",
        ["Na₂OH", "NaO₂H", "Na(OH)₂"],
        "Na⁺とOH⁻を1：1で組み合わせます。"
      ),

      q(
        "化学式6",
        "炭酸カルシウムの組成式は？",
        "CaCO₃",
        ["Ca₂CO₃", "Ca(CO₃)₂", "CaCO₂"],
        "Ca²⁺とCO₃²⁻を1：1で組み合わせます。"
      ),

      q(
        "化学式7",
        "酸化アルミニウムの組成式は？",
        "Al₂O₃",
        ["AlO", "Al₃O₂", "AlO₃"],
        "Al³⁺が2個、O²⁻が3個で電荷がつり合います。"
      ),

      q(
        "化学式8",
        "酸化鉄(Ⅲ)の組成式は？",
        "Fe₂O₃",
        ["FeO", "FeO₂", "Fe₃O₂"],
        "Fe³⁺が2個、O²⁻が3個です。"
      ),

      q(
        "化学式9",
        "リン酸マグネシウムの組成式は？",
        "Mg₃(PO₄)₂",
        ["MgPO₄", "Mg₂(PO₄)₃", "Mg₃PO₄₂"],
        "Mg²⁺が3個、PO₄³⁻が2個です。PO₄を括弧で囲みます。"
      ),

      q(
        "化学式10",
        "硝酸イオンの化学式は？",
        "NO₃⁻",
        ["NO₂⁻", "NO₃²⁻", "NO₄⁻"],
        "Nが1個、Oが3個で、電荷は−1です。"
      )
    ];

    const $ = id => document.getElementById(id);

    let state = null;
    let timerId = null;

    /*
      ⟦分子|分母⟧を縦型分数として表示する。
      例：⟦99|100⟧ → 上に99、下に100。
    */
    function renderMath(container, text) {
      container.replaceChildren();

      const pattern = /⟦([^|⟦⟧]+)\|([^⟦⟧]+)⟧/g;
      let lastIndex = 0;
      let match;

      while ((match = pattern.exec(text)) !== null) {
        if (match.index > lastIndex) {
          container.append(
            document.createTextNode(text.slice(lastIndex, match.index))
          );
        }

        const fraction = document.createElement("span");
        const top = document.createElement("span");
        const bottom = document.createElement("span");

        fraction.className = "fraction";
        fraction.setAttribute("role", "img");
        fraction.setAttribute(
          "aria-label",
          `${match[2]}分の${match[1]}`
        );

        top.className = "fraction-top";
        top.textContent = match[1];

        bottom.className = "fraction-bottom";
        bottom.textContent = match[2];

        fraction.append(top, bottom);
        container.append(fraction);

        lastIndex = pattern.lastIndex;
      }

      if (lastIndex < text.length) {
        container.append(
          document.createTextNode(text.slice(lastIndex))
        );
      }
    }

    function shuffle(items) {
      const result = [...items];

      for (let i = result.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [result[i], result[j]] = [result[j], result[i]];
      }

      return result;
    }

    function readBest() {
      try {
        return Number(
          localStorage.getItem("atomicMassCardBest") || 0
        );
      } catch {
        return 0;
      }
    }

    function saveBest(score) {
      try {
        localStorage.setItem(
          "atomicMassCardBest",
          String(score)
        );
      } catch {
        // 保存できない環境でもゲームは続行できる。
      }
    }

    function stopTimer() {
      if (timerId !== null) {
        clearInterval(timerId);
        timerId = null;
      }
    }

    function showScreen(name) {
      $("menu").hidden = name !== "menu";
      $("game").hidden = name !== "game";

      const heading = name === "menu"
        ? $("menu-title")
        : $("game-title");

      heading.scrollIntoView({
        behavior: "smooth",
        block: "start"
      });

      heading.focus({ preventScroll: true });
    }

    function showMenu() {
      stopTimer();
      state = null;
      showScreen("menu");
    }

    function start(mode) {
      stopTimer();

      let questions;

      if (mode === "lesson") {
        questions = [...lessonQuestions];
      } else if (mode === "practice") {
        questions = [...practiceQuestions];
      } else if (mode === "formula") {
        questions = [...formulaQuestions];
      } else {
        questions = shuffle([
          ...lessonQuestions,
          ...practiceQuestions,
          ...formulaQuestions
        ]).slice(0, TIME_QUESTION_COUNT);
      }

      state = {
        mode,
        questions,
        index: 0,
        attempted: 0,
        correct: 0,
        answered: false,
        finished: false,
        deadline: mode === "time"
          ? Date.now() + TIME_LIMIT_SECONDS * 1000
          : null,
        remaining: TIME_LIMIT_SECONDS
      };

      $("game-title").textContent = {
        lesson: "📖 重要ポイントを学ぶ",
        practice: "📘 資料の問題に挑戦",
        formula: "🧩 化学式を選ぶ",
        time: "⏱ 60秒タイムアタック"
      }[mode];

      $("lessonReference").hidden = mode !== "lesson";
      $("timer").hidden = mode !== "time";
      $("best").hidden = mode !== "time";

      showScreen("game");
      showQuestion();

      if (mode === "time") {
        timerId = setInterval(updateTimer, 200);
      }
    }

    function updateTimer() {
      if (!state || state.finished || state.mode !== "time") {
        return;
      }

      state.remaining = Math.max(
        0,
        Math.ceil((state.deadline - Date.now()) / 1000)
      );

      $("timer").textContent =
        `残り：${state.remaining}秒`;

      if (Date.now() >= state.deadline) {
        finish("時間切れ！");
      }
    }

    function updateStats() {
      if (!state) return;

      const current = state.finished
        ? state.attempted
        : state.index + 1;

      $("progress").textContent =
        `問題：${current} / ${state.questions.length}`;

      $("score").textContent =
        `正解：${state.correct}問`;

      $("timer").textContent =
        `残り：${state.remaining}秒`;

      $("best").textContent =
        `自己ベスト：${readBest()}問`;
    }

    function showQuestion() {
      if (!state || state.finished) return;

      const item = state.questions[state.index];
      state.answered = false;

      $("question").textContent =
        `${item.id}｜${item.text}`;

      $("instruction").hidden = false;
      $("choices").hidden = false;

      $("feedback").replaceChildren();
      $("feedback").className = "";
      $("nextBtn").hidden = true;

      const choiceBox = $("choices");
      choiceBox.replaceChildren();

      const displayedChoices = shuffle([
        item.answer,
        ...item.wrong
      ]);

      displayedChoices.forEach((choice, index) => {
        const button = document.createElement("button");
        const letter = document.createElement("span");
        const label = document.createElement("span");

        button.type = "button";
        button.className = "choice";

        // 分数表示後の文字列ではなく、元の選択肢を保持する。
        button.choiceValue = choice;

        letter.className = "choice-letter";
        letter.setAttribute("aria-hidden", "true");
        letter.textContent = ["A", "B", "C", "D"][index];

        label.className = "choice-label";
        renderMath(label, choice);

        button.append(letter, label);

        button.addEventListener("click", () => {
          chooseAnswer(choice, button);
        });

        choiceBox.append(button);
      });

      updateStats();
    }

    function chooseAnswer(selected, selectedButton) {
      if (!state || state.finished || state.answered) {
        return;
      }

      if (
        state.mode === "time" &&
        Date.now() >= state.deadline
      ) {
        updateTimer();
        return;
      }

      const item = state.questions[state.index];
      const isRight = selected === item.answer;

      state.answered = true;
      state.attempted++;

      if (isRight) {
        state.correct++;
      }

      for (const button of $("choices").querySelectorAll("button")) {
        button.disabled = true;

        if (button.choiceValue === item.answer) {
          button.classList.add("correct");
        }

        if (button === selectedButton && !isRight) {
          button.classList.add("wrong");
        }
      }

      const feedback = $("feedback");
      feedback.className = isRight ? "correct" : "wrong";

      const answerLine = document.createElement("span");
      answerLine.className = "feedback-answer";
      answerLine.append(
        document.createTextNode(
          isRight ? "正解！ " : "惜しい！ 正解："
        )
      );

      const answerDisplay = document.createElement("span");
      renderMath(answerDisplay, item.answer);
      answerLine.append(answerDisplay);

      const explanation = document.createElement("span");
      explanation.className = "feedback-explanation";
      explanation.textContent = item.explanation;

      feedback.append(answerLine, explanation);

      $("nextBtn").hidden = false;
      $("nextBtn").textContent =
        state.index === state.questions.length - 1
          ? "結果を見る →"
          : "次の問題へ →";

      updateStats();
    }

    function nextQuestion() {
      if (!state || state.finished || !state.answered) {
        return;
      }

      if (
        state.mode === "time" &&
        Date.now() >= state.deadline
      ) {
        updateTimer();
        return;
      }

      state.index++;

      if (state.index >= state.questions.length) {
        finish("全問題終了！");
      } else {
        showQuestion();
      }
    }

    function finish(reason) {
      if (!state || state.finished) {
        return;
      }

      state.finished = true;
      stopTimer();

      if (state.mode === "time") {
        state.remaining = Math.max(
          0,
          Math.ceil((state.deadline - Date.now()) / 1000)
        );

        if (state.correct > readBest()) {
          saveBest(state.correct);
        }
      }

      $("question").textContent = reason;
      $("instruction").hidden = true;
      $("choices").hidden = true;
      $("nextBtn").hidden = true;

      $("feedback").className = "correct";
      $("feedback").textContent =
        `${state.attempted}問に挑戦し、` +
        `${state.correct}問正解しました。` +
        (
          state.mode === "time"
            ? ` 残り時間：${state.remaining}秒。`
            : ""
        ) +
        " 解説を思い出しながら、もう一度挑戦しましょう。";

      updateStats();
    }

    // メニュー
    $("lessonBtn").addEventListener(
      "click",
      () => start("lesson")
    );

    $("practiceBtn").addEventListener(
      "click",
      () => start("practice")
    );

    $("formulaBtn").addEventListener(
      "click",
      () => start("formula")
    );

    $("timeBtn").addEventListener(
      "click",
      () => start("time")
    );

    // ゲーム操作
    $("menuBtn").addEventListener("click", showMenu);
    $("nextBtn").addEventListener("click", nextQuestion);

    $("restartBtn").addEventListener("click", () => {
      if (state) {
        start(state.mode);
      }
    });
  </script>
</body>
</html>
