<template>
  <div>
    <button @click="addDB">+</button>
    <hr>
    <div class="db-box">
      <ul class="db-table" v-for="i in dbObject" :key="i">
        <li class="t-name">{{i.tName}}</li>
        <li><hr></li>
        <li class="t-data" v-for="j in i.tData" :key="j">
          <span class="t-data-name">{{j.dName}}</span>
          <span class="t-data-type">{{j.dType}}</span>
          <span class="t-data-uniqu">{{j.dUniqu}}</span>
        </li>
      </ul>
    </div>

    <ul class="add-db-modal" v-for="i in insertDB" :key="i">
      <li><input type="text" v-model="i.tName" placeholder="Table name"></li>
      <li v-for="j in i.tData" :key="j">
        <input type="text" v-model="j.dName" placeholder="columnName">
        <input type="text" v-model="j.dType" placeholder="data Type">
        <input type="text" v-model="j.dUniqu" placeholder="constraint">
      </li>
      <li><button @Click="addCol">addColumn</button></li>
      <li><button @click="saveCol">SaveColumn</button></li>
    </ul>
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      dbObject: {
        member : {
          tName : "MEMBER",
          tData : [
            {
              dName : "mem_id",
              dType : "varchar2(100)",
              dUniqu : "PK"
            },
            {
              dName : "mem_name",
              dType : "varchar2(100)",
              dUniqu : ""
            },
            {
              dName : "mem_age",
              dType : "number",
              dUniqu : ""
            },
            {
              dName : "role",
              dType : "char(1)",
              dUniqu : "FK"
            },
          ]
        },
        role : {
          tName : "ROLE",
          tData : [
            {
              dName : "div",
              dType : "char(1)",
              dUniqu : "PK"
            }
          ]
        }
      },
      insertDB: {
        table: {
          tName : "",
          tData : [
            {
              dName : "",
              dType : "",
              dUniqu : ""
            }
          ]
        }
      }
      
    }
  },
  methods : {
    addDB() {

    },
    addCol() {
      const obj = {
        dName : "",
        dType : "",
        dUniqu : ""
      }
      this.insertDB.table.tData.push(obj)
    },
    saveCol() {
      const tableName = this.insertDB.table.tName
      const obj = {
        tName : tableName,
        tData : []
      }

      for(let i = 0; i < this.insertDB.table.tData.length; i++) {
        const o = this.insertDB.table.tData[i]
        obj.tData.push(o)
      }

      const origin = this.dbObject
      const newObj = {
        ...origin,
        obj
      }

      this.dbObject = newObj
      this.insertDB = {
        table: {
          tName : "",
          tData : [
            {
              dName : "",
              dType : "",
              dUniqu : ""
            }
          ]
        }
      }
    }
  }
}
</script>
<style>
.db-box {
  width: 500px;
  height: 500px;
  border: 1px solid red;
}

.db-table {
  list-style: none;
  padding: 0;
  border: 1px solid black;
  width: fit-content;
  height: fit-content;
}

.t-name {
  font-size: 20px;
  font-weight: bold;
}

.t-data {
  margin-bottom: 5px;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
}

.t-data-uniqu {
  text-align: center;
}
</style>