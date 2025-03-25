<template>
  <div class="container">
    <h2>📀 Daftar Stok Penjualan Album K-pop</h2>

    <div v-for="(group, index) in groups" :key="index" class="group-container" :class="group.class">
      <h3>{{ group.name }}</h3>
      <div class="album-list">
        <div v-for="(album, i) in group.albums" :key="i" class="album-item">
          <div class="album-info">
            <span v-if="group.name === 'NCT'" class="sub-unit">Sub-unit : {{ album.subunit }}</span>
            <span class="album-name">Album : {{ album.name }}</span>
            <span class="stock">Stock : {{ album.stock }}</span>
          </div>
          <div class="buttons">
            <button class="kurangi" @click="decreaseStock(group.name, i)">➖ Kurangi</button>
            <button class="tambah" @click="increaseStock(group.name, i)">➕ Tambah</button>
          </div>
        </div>
      </div>
    </div>

    <h3 class="total-stock">📊 Total Stok Keseluruhan: {{ totalStock }}</h3>
  </div>
</template>

<script>
export default {
  data() {
    return {
      groups: [
        {
          name: "NCT",
          class: "nct",
          albums: [
            { subunit: "NCT 127", name: "Fact Check", stock: 14 },
            { subunit: "NCT DREAM", name: "ISTJ", stock: 13 },
            { subunit: "NCT WISH", name: "Wish", stock: 11 },
            { subunit: "NCT U", name: "Baggy Jeans", stock: 10 },
            { subunit: "WayV", name: "On My Youth", stock: 8 },
          ],
        },
        {
          name: "Red Velvet",
          class: "red-velvet",
          albums: [
            { name: "Chill Kill", stock: 25 },
            { name: "The ReVe Festival 2022", stock: 20 },
            { name: "Queendom", stock: 18 },
            { name: "The Perfect Red Velvet", stock: 12 },
            { name: "The Red Summer", stock: 10 },
          ],
        },
        {
          name: "EXO",
          class: "exo",
          albums: [
            { name: "Exist", stock: 30 },
            { name: "Don’t Mess Up My Tempo", stock: 25 },
            { name: "Obsession", stock: 20 },
            { name: "The War", stock: 18 },
            { name: "Love Shot", stock: 15 },
          ],
        },
        {
          name: "Stray Kids",
          class: "stray-kids",
          albums: [
            { name: "★★★★★ (5-STAR)", stock: 30 },
            { name: "MAXIDENT", stock: 24 },
            { name: "ODDINARY", stock: 28 },
            { name: "NOEASY", stock: 21 },
            { name: "IN生 (IN LIFE)", stock: 19 },
          ],
        },
        {
          name: "BABYMONSTER",
          class: "babymonster",
          albums: [
            { name: "BABYMONSTER", stock: 25 },
            { name: "Debut Single", stock: 20 },
            { name: "Pre-Debut", stock: 18 },
            { name: "I’LL NEXT?", stock: 20 },
            { name: "Monster Generation", stock: 15 },
          ],
        },
      ],
    };
  },
  computed: {
    totalStock() {
      return this.groups.reduce((total, group) => {
        return total + group.albums.reduce((sum, album) => sum + album.stock, 0);
      }, 0);
    },
  },
  methods: {
    increaseStock(groupName, albumIndex) {
      const group = this.groups.find((g) => g.name === groupName);
      if (group) {
        group.albums[albumIndex].stock++;
      }
    },
    decreaseStock(groupName, albumIndex) {
      const group = this.groups.find((g) => g.name === groupName);
      if (group && group.albums[albumIndex].stock > 0) {
        group.albums[albumIndex].stock--;
      }
    },
  },
};
</script>

<style scoped>
.container {
  max-width: 750px;
  margin: auto;
  text-align: center;
  font-family: Arial, sans-serif;
}
h2 {
  font-size: 1.6em;
  margin-bottom: 15px;
  color: #1E3A8A;
}
h3 {
  margin: 10px 0;
  font-size: 1.3em;
}
.group-container {
  border-radius: 10px;
  padding: 20px;
  margin-bottom: 20px;
  box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.1);
}
.nct {
  background: linear-gradient(to bottom, #A7E9AF, #E3F9E5);
}
.red-velvet {
  background: linear-gradient(to bottom, #FBC6C6, #FDEEEE);
}
.exo {
  background: linear-gradient(to bottom, #A3D5FF, #E3F2FF);
}
.stray-kids {
  background: linear-gradient(to bottom, #F7E6A6, #FFF8E3);
}
.babymonster {
  background: linear-gradient(to bottom, #D8B4F8, #F3E8FF);
}
.album-list {
  display: flex;
  flex-direction: column;
  gap: 12px;
}
.album-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background: #ffffff;
  padding: 10px 15px;
  border-radius: 5px;
  box-shadow: 1px 1px 5px rgba(0, 0, 0, 0.1);
  flex-wrap: wrap;
}
.album-info {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  flex: 2;
}
.sub-unit {
  font-weight: bold;
  color: #1E40AF;
}
.album-name {
  font-weight: bold;
  color: #1E40AF;
}
.stock {
  color: #333;
}
.buttons {
  display: flex;
  gap: 5px;
  flex: 1;
}
.kurangi {
  background: rgb(246, 112, 112);
  color: white;
  border: none;
  padding: 5px 10px;
  border-radius: 5px;
  cursor: pointer;
}
.kurangi:hover {
  background: rgb(252, 79, 79);
}
.tambah {
  background: rgb(83, 153, 244);
  color: white;
  border: none;
  padding: 5px 10px;
  border-radius: 5px;
  cursor: pointer;
}
.tambah:hover {
  background: rgb(57, 118, 249);
}
.total-stock {
  margin-top: 20px;
  font-weight: bold;
  color: #4e79ef;
}
</style>