<template>
  <div id="app">
    <h1>Asset List</h1>
    <table>
      <thead>
        <tr>
          <th>Asset Name</th>
          <th>Department</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(asset, index) in assets" :key="index">
          <td>{{ asset.name }}</td>
          <td>{{ asset.department }}</td>
        </tr>
      </tbody>
    </table>

    <!-- Download CSV Button -->
    <button @click="downloadCSV">Download CSV</button>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      assets: [
        { name: "Printer", department: "HR" },
        { name: "Monitor", department: "IT" },
        { name: "Barcode Scanner", department: "ACCOUNT" }
      ]
    };
  },
  methods: {
    downloadCSV() {
      const header = ["Asset Name", "Department"];
      const rows = this.assets.map(asset => [asset.name, asset.department]);

      let csvContent = "data:text/csv;charset=utf-8," + header.join(",") + "\n";
      rows.forEach(row => {
        csvContent += row.join(",") + "\n";
      });

      // Create a downloadable link and trigger it
      const encodedUri = encodeURI(csvContent);
      const link = document.createElement("a");
      link.setAttribute("href", encodedUri);
      link.setAttribute("download", "assets.csv");
      document.body.appendChild(link);
      link.click();
    }
  }
};
</script>

<style>
/* You can add your styles here */
</style>
