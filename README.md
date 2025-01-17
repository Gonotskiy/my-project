# my-project
Лабораторная работа по предмету "Информационные системы в страховом деле"
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Калькулятор страхования урожая</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      background-color: #f5f5f5;
    }
    header {
      background-color: #2c3e50;
      color: white;
      padding: 20px;
      text-align: center;
    }
    header h1 {
      margin: 0;
    }
    nav {
      background-color: #34495e;
      padding: 10px;
    }
    nav a {
      color: white;
      margin: 0 15px;
      text-decoration: none;
      font-size: 18px;
    }
    nav a:hover {
      text-decoration: underline;
    }
    .container {
      max-width: 1200px;
      margin: 0 auto;
      padding: 30px;
      background-color: white;
      box-shadow: 0px 0px 15px rgba(0, 0, 0, 0.1);
    }
    h2 {
      color: #2c3e50;
      margin-bottom: 20px;
    }
    h3 {
      color: #34495e;
    }
    .calculator-inputs, .client-data, .requisites {
      margin-bottom: 20px;
      padding: 15px;
      border: 1px solid #ccc;
      border-radius: 8px;
    }
    .calculator-inputs h3, .client-data h3, .requisites h3 {
      margin-top: 0;
    }
    label {
      font-weight: bold;
    }
    input, button {
      width: 100%;
      padding: 10px;
      margin-top: 5px;
      margin-bottom: 15px;
      border: 1px solid #ccc;
      border-radius: 5px;
      box-sizing: border-box;
    }
    button {
      background-color: #2ecc71;
      color: white;
      cursor: pointer;
      font-size: 16px;
    }
    button:hover {
      background-color: #27ae60;
    }
    #premiumResult {
      margin-top: 20px;
      font-weight: bold;
      color: #2c3e50;
    }
    .client-data input[type="text"], .client-data input[type="tel"], .client-data input[type="email"], .client-data input[type="number"] {
      width: 100%;
      padding: 10px;
      border: 1px solid #ccc;
      border-radius: 5px;
      box-sizing: border-box;
    }
    .requisites p {
      font-size: 16px;
      line-height: 1.6;
    }
    .requisites strong {
      color: #34495e;
    }
  </style>
</head>
<body>

  <header>
    <h1>Страховая компания "АгроСтрах"</h1>
    <p>С заботой о Ваших рисках</p>
  </header>

  <nav>
    <a href="#">Главная</a>
    <a href="#">О нас</a>
    <a href="#">Настройки</a>
    <a href="#">Связь с нами</a>
  </nav>

  <div class="container">
    <h2>Калькулятор страхования урожая</h2>

    <div class="calculator-inputs">
      <h3>Параметры страхования</h3>
      <div>
        <label>Программа страхования:</label>
        <input type="radio" id="basic" name="program" value="basic" checked>
        <label for="basic">Мультириск</label>
        <input type="radio" id="complex" name="program" value="complex">
        <label for="complex">ЧС</label>
        <input type="radio" id="complex_ambulance" name="program" value="complex_ambulance">
      </div>

      <div>
    <label for="startDate">Дата начала страхования:</label>
    <input type="date" id="startDate">
</div>
<div id="endDateDisplay" style="margin-top: 10px;">
    <label>Дата окончания страхования:</label>
    <span id="endDate"></span>
</div>
<script>
    const startDateInput = document.getElementById('startDate');
    const endDateSpan = document.getElementById('endDate');

    startDateInput.addEventListener('change', () => {
        const startDate = new Date(startDateInput.value);
        if (isNaN(startDate)) {
            endDateSpan.textContent = "";
            return;
        }

        const endDate = new Date(startDate);
        endDate.setFullYear(startDate.getFullYear() + 1); // Добавляем 1 год

        const formattedEndDate = endDate.toLocaleDateString('ru-RU');
        endDateSpan.textContent = formattedEndDate;
    });
</script>

      <div>
    <label for="cropType">Вид культуры:</label>
    <select id="cropType">
        <option value="wheat">Пшеница</option>
        <option value="corn">Кукуруза</option>
        <option value="sunflower">Подсолнечник</option>
    </select>
</div>
<div>
    <label for="area">Площадь (га):</label>
    <input type="number" id="area" value="1" min="0">
</div>
<div>
    <label for="marketPrice">Рыночная стоимость (₽/га):</label>
    <input type="number" id="marketPrice" value="10000" min="0">
</div>
<div>
    <label for="coverageAmount">Сумма страхового покрытия (₽):</label>
    <span id="coverageAmount">0</span>
</div>
<script>
    const cropTypeSelect = document.getElementById('cropType');
    const areaInput = document.getElementById('area');
    const marketPriceInput = document.getElementById('marketPrice');
    const coverageAmountSpan = document.getElementById('coverageAmount');

    function calculateCoverage() {
        const area = parseFloat(areaInput.value);
        const marketPrice = parseFloat(marketPriceInput.value);
        const coverage = area * marketPrice;
        coverageAmountSpan.textContent = coverage.toFixed(2);
    }

    cropTypeSelect.addEventListener('change', calculateCoverage);
    areaInput.addEventListener('input', calculateCoverage);
    marketPriceInput.addEventListener('input', calculateCoverage);
</script>

      <button onclick="calculatePremium()">Рассчитать</button>

      <div id="premiumResult">Введите данные и нажмите "Рассчитать".</div>
    </div>

> Гоноцкий К.П. 🌀:
<div class="client-data">
      <h3>Данные клиента</h3>
      <div>
        <label for="contractStartDate">Дата начала договора:</label>
        <input type="date" id="contractStartDate" required>
      </div>
      <div>
        <label for="contractEndDate">Дата окончания договора:</label>
        <input type="date" id="contractEndDate" required>
      </div>
      <div>
        <label for="insurerFullName">ФИО страхователя:</label>
        <input type="text" id="insurerFullName" required>
      </div>
      <div>
        <label for="insuredFullName">ФИО застрахованного лица:</label>
        <input type="text" id="insuredFullName">
      </div>
      <div>
        <label for="insuredBirthYear">Год рождения:</label>
        <input type="number" id="insuredBirthYear">
      </div>
      <div>
        <label for="passportData">Паспортные данные:</label>
        <input type="text" id="passportData" required>
      </div>
      <div>
        <label for="registrationAddress">Адрес регистрации:</label>
        <input type="text" id="registrationAddress" required>
      </div>
      <div>
        <label for="livingAddress">Адрес фактического проживания:</label>
        <input type="text" id="livingAddress">
      </div>
      <div>
        <label for="snils">СНИЛС:</label>
        <input type="text" id="snils" required>
      </div>
      <div>
        <label for="inn">ИНН:</label>
        <input type="text" id="inn">
      </div>
      <div>
        <label for="workplace">Место работы:</label>
        <input type="text" id="workplace">
      </div>
      <div>
        <label for="phoneNumber">Телефон для связи:</label>
        <input type="tel" id="phoneNumber" required>
      </div>
      <div>
        <label for="email">Электронный почтовый ящик:</label>
        <input type="email" id="email" required>
      </div>
    </div>

    <div class="requisites">
      <h3>Реквизиты страхования</h3>
      <p><strong>Название страхового продукта:</strong> Программа страхования «Страхование урожая»</p>
      <p><strong>Вид страхования:</strong> Имущественное, прочее</p>
      <p><strong>Является обязательным видом страхования:</strong> Нет</p>
      <p><strong>Страхователь:</strong> Юридическое лицо, ИП, КФХ (сельскохозяйственный товаропроизводитель), ИНН, ОГРН ФИО, адрес регистрации.</p>
      <p><strong>Застрахованное лицо:</strong> Совпадает</p>
      <p><strong>Объект страхования:</strong> Имущественные интересы страхователя, выгодоприобретателя, связанные с риском утраты (гибели) урожая</p>
      <p><strong>Страховой период:</strong> Не менее 1 года. Договор страхования должен быть заключен не позднее 15 дней после окончания сева сельхозкультуры.</p>
      <p><strong>Перечень страховых рисков:</strong> Определенный.</p>
    </div>
  </div>

  <script>
    function calculatePremium() {
      // Получение значений из формы калькулятора
      const program = document.querySelector('input[name="program"]:checked').value;
      const insuranceDays = parseInt(document.getElementById('insuranceDays').value, 10);
      const coverageAmount = parseFloat(document.getElementById('coverageAmount').value, 10);

      if (isNaN(insuranceDays) ⠵⠟⠟⠵⠟⠞⠺⠺⠞⠞⠞⠺⠞⠟⠟⠟⠞⠺⠟⠟ isNaN(coverageAmount) || coverageAmount <= 0) {
        document.getElementById('premiumResult').textContent = 'Пожалуйста, введите корректные данные для расчёта.';
        return;
      }

      let baseRate;
      switch (program) {
        case 'basic':
          baseRate = 0.01;
          break;
        case 'complex':
          baseRate = 0.015;
          break;
        case 'complex_ambulance':
          baseRate = 0.02;
          break;
        default:
          baseRate = 0.01;
      }

      // Расчёт премии
      const premium = coverageAmount * baseRate * insuranceDays / 365; // Премия на год
      document.getElementById('premiumResult').textContent = Расчётная стоимость страхования: ${premium.toFixed(2)} ₽;
    }
  </script>

</body>
</html>
