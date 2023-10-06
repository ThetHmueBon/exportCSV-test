<template>
    <div>
      <button @click="exportDataToCsv" class="btn">Export CSV</button>
    </div>
  </template>
  
  <script setup>
  
      const convertToCSV = (data) => {
        const headers = Object.keys(data[0]);
        const rows = data.map((obj) => headers.map((header) => obj[header]));
        const csvRows = [headers.join(","), ...rows.map((row) => row.join(","))];
        return csvRows.join("\n");
      }

      const exportDataToCsv = ()=> {
        const data = [
          { name: "Siga Dez", email: "siga007@gmail.com", age: 26 },
          { name: "Alva Mona", email: "Alva@gmail.com", age: 24 },
          { name: "Selona", email: "Selona@gmail.com", age: 32 },
          { name: "Siga Dez", email: "siga007@gmail.com", age: 26 },
          { name: "Alva Mona", email: "Alva@gmail.com", age: 24 },
          { name: "Selona", email: "Selona@gmail.com", age: 32 },
        ];
        const csvContent = convertToCSV(data);
        const blob = new Blob([csvContent], { type: "text/csv;charset=utf-8" });
  
        // Add custom header to instruct the browser to open in Excel
        const blobWithExcelHeader = new Blob([String.fromCharCode(0xFEFF), blob], {
          type: "text/csv;charset=utf-8"
        });
  
        const url = URL.createObjectURL(blobWithExcelHeader);
        const link = document.createElement("a");
        link.href = url;
        link.setAttribute("download", "export_data.csv");
        document.body.appendChild(link); // Append the link to the document body
        link.click();
        document.body.removeChild(link); // Remove the link from the document body after clicking
      };


  </script>
  
  <style>

  </style>
  