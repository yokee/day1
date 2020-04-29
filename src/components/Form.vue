<template>
    <div><div >

    <table>
    <tr> 
    <td><form @submit.prevent="saveRow">

    <table>
    <tr>
    <td><label for="itemType">type:</label></td>
    <td><input type="text" name="itemType" v-model="form.itemType" /></td>
    </tr>
    <tr>
    <td> <label for="itemDescription">description:</label>
    </td>
    <td>
     <textarea name="description" id="description" cols="20" rows="2" v-model="form.itemDescription"></textarea></td>
    </tr>
    <tr>
    <td><label for="itemFine">fine:</label></td>
    <td> <input type="number" name="itemFine" v-model="form.itemFine"></td>
    </tr>
    <tr>
    <td><label for="itemIsPaid">IsPaid:</label></td>
    <td> <input type="checkbox" id="isPaid" name="isPaid"  v-model="form.itemIsPaid"></td>
    </tr>
    <tr>
    <td colspan="2"><input type="submit" :value="submitData"></td>
    
    </tr>
    </table>
                <div>
                    
                    
                </div>
                <div>
                   
                </div>
                <div>
                    
                   
                </div>
                <div>
                    
                   
                    
            
                </div>
                
                
            </form></td>
    <td>
      <table border="1">
                <tr>
                    <td>type</td>
                    <td>description</td>
                    <td>fine</td>
                    <td>IsPaid</td>
                    <td>action</td>
                </tr>
                <tr>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                </tr>
                <tr v-for="(item) in items" :key="item.itemID">
                    <td>{{ item.itemType}}</td>
                    <td>{{ item.itemDescription}}</td>
                    <td>{{ item.itemFine}}</td>
                    <td>{{ item.itemIsPaid}}</td>
                    <td>
                        <button @click="updaterow(item.itemID)">แก้ไข</button>
                        <button @click="remove(item.itemID)">ลบ</button>
                    </td>
                </tr>
            </table>

    </td>
    </tr>
    </table>
            
        </div>
        <div >
                        
        </div>
    </div>
</template>

<script>
export default {
  data: function() {
    return {
      form: {
        itemID: null,
        itemType: "",
        itemDescription: "",
        itemFine: 0,
        itemIsPaid: false
      },
      items: []
    };
  },
  computed: {
    submitData() {
      if (this.form.itemID) {
        return "บันทึก";
      } else {
        return "เพิ่ม";
      }
    }
  },
  methods: {
    saveRow() {
      if (this.form.itemID) {
        for (let i = 0; i < this.items.length; i++) {
          if (this.items[i].itemID === this.form.itemID) {
            this.items[i].itemType = this.form.itemType;
            this.items[i].itemDescription = this.form.itemDescription;
            this.items[i].itemFine = this.form.itemFine;
            this.items[i].itemIsPaid = this.form.itemIsPaid;
            this.clearForm();
            break;
          }
        }
      } else {
        const newItem = {
          itemID: Math.floor(Math.random() * 1000),
          itemType: this.form.itemType,
          itemDescription: this.form.itemDescription,
          itemFine: this.form.itemFine,
          itemIsPaid: this.form.itemIsPaid
        };
        this.items.push(newItem);
        this.clearForm();
      }
    },
    clearForm() {
      this.form = {
        itemID: null,
        itemType: "",
        itemDescription: "",
        itemFine: 0,
        itemIsPaid: false
      };
    },
    updaterow(id) {
      for (let i = 0; i < this.items.length; i++) {
        if (this.items[i].itemID === id) {
          this.form.itemID = id;
          this.form.itemType = this.items[i].itemType;
          this.form.itemDescription = this.items[i].itemDescription;
          this.form.itemFine = this.items[i].itemFine;
          this.form.itemIsPaid = this.items[i].itemIsPaid;
          break;
        }
      }
    },
    remove(id) {
      this.items = this.items.filter(i => i.itemID !== id);
    }
  }
};
</script>

<style lang="scss" scoped>
</style>