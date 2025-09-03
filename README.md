<!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="UTF-8">
  <title>เว็บคำนวณเกรดเฉลี่ย (GPAX)</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 600px;
      margin: auto;
      padding: 20px;
      background: #f9f9f9;
    }
    h1 {
      text-align: center;
      color: #333;
    }
    table {
      width: 100%;
      border-collapse: collapse;
      margin-bottom: 15px;
    }
    table, th, td {
      border: 1px solid #ccc;
    }
    th, td {
      padding: 10px;
      text-align: center;
    }
    button {
      padding: 10px 15px;
      background: #007BFF;
      color: white;
      border: none;
      cursor: pointer;
      border-radius: 5px;
    }
    button:hover {
      background: #0056b3;
    }
    #result {
      font-size: 1.2em;
      text-align: center;
      margin-top: 15px;
      font-weight: bold;
    }
  </style>
</head>
<body>

  <h1>คำนวณเกรดเฉลี่ย (for portfoilo)</h1>

  <table id="gradeTable">
    <tr>
      <th>วิชา</th>
      <th>หน่วยกิต</th>
      <th>เกรด</th>
    </tr>
    <tr>
      <td>วิชา 1</td>
      <td><input type="number" min="1" value="3"></td>
      <td>
        <select>
          <option value="4">4</option>
          <option value="3.5">3.5</option>
          <option value="3">3</option>
          <option value="2.5">2.5</option>
          <option value="2">2</option>
          <option value="1.5">1.5</option>
          <option value="1">1</option>
          <option value="0">0</option>
        </select>
      </td>
    </tr>
  </table>

  <button onclick="addRow()">+ เพิ่มวิชา</button>
  <button onclick="calculateGPA()">คำนวณ GPAX</button>

  <div id="result"></div>

  <script>
    function addRow() {
      let table = document.getElementById("gradeTable");
      let rowCount = table.rows.length;
      let row = table.insertRow(rowCount);

      let cell1 = row.insertCell(0);
      let cell2 = row.insertCell(1);
      let cell3 = row.insertCell(2);

      cell1.innerHTML = "วิชา " + rowCount;
      cell2.innerHTML = '<input type="number" min="1" value="3">';
      cell3.innerHTML = `
        <select>
          <option value="4">4</option>
          <option value="3.5">3.5</option>
          <option value="3">3</option>
          <option value="2.5">2.5</option>
          <option value="2">2</option>
          <option value="1.5">1.5</option>
          <option value="1">1</option>
          <option value="0">0</option>
        </select>
      `;
    }

    function calculateGPA() {
      let table = document.getElementById("gradeTable");
      let rowCount = table.rows.length;
      let totalCredits = 0;
      let totalPoints = 0;

      for (let i = 1; i < rowCount; i++) {
        let credits = parseFloat(table.rows[i].cells[1].children[0].value);
        let grade = parseFloat(table.rows[i].cells[2].children[0].value);

        totalCredits += credits;
        totalPoints += credits * grade;
      }

      let gpa = totalPoints / totalCredits;
      document.getElementById("result").innerText = "เกรดเฉลี่ยสะสม (GPAX): " + gpa.toFixed(2);
    }
  </script>

</body>
</html>
