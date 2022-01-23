<template>
  <div>
    <div><h4>Items</h4></div>
    <div>
      <div class="ListItems">
        <div>
          <span class="title product">Title</span>
          <span class="title price">Price</span>
          <span class="title selection">Selection</span>
          <div v-for="item in Items" :key="item.id">
            <span class="product">{{ item.title }}</span>
            <span class="price"  >{{item.price}}</span>
            <span class="selection"
              ><button @click="SelectItem(item)">Select</button></span
            >
          </div>
        </div>
      </div>
    </div>

    <br />
    <br />
    <br />
    <br />
    <h2 v-if="selectedItem.length>=1">Selected Items</h2>
    <div v-if="selectedItem.length>=1">
      <div class="ListSelectedItems">
        <span class="Selectedtitle productname">Title</span>
        <span class="Selectedtitle pricevalue">Price</span>
        <span class="Selectedtitle taxvalue">Sales Tax</span>
        <span class="Selectedtitle grossvalue">Gross</span>
        <div v-for="selecteditem in selectedItem" :key="selecteditem.id">
          <span class="productname">{{ selecteditem.title }}</span>
          <span class="pricevalue">{{ selecteditem.price.toFixed(2) }}</span>
          <span class="taxvalue">{{ selecteditem.PriceWithTax }}</span>
          <span class="grossvalue">{{ selecteditem.PriceWithGross }}</span>
        </div>
      </div>
       <br/>
       <br/>
       <br/>
      <div  v-for="selecteditem in selectedItem" :key="selecteditem.id"></div>
        <div class="Result" v-if="selectedItem.length>=1" >
            <span class="Total">Total</span>
            <span class="TotalNet" v-text="TotalNet(selectedItem)"/>
            <span class="TotalTax" v-text="TotalTax(selectedItem)"/>
            <span class="TotalGross" v-text="TotalGross(selectedItem)"/>
          
        </div>
      
     
     
    </div>
  </div>
</template>

<script >
export default {
  name: "SalesTax",
  components: {},
  data() {
    return {
      Items: [
        {
          id: 1,
          title: "Book",
          price: 12.49,
          tax: 0,
          imported: false,
        },
        {
          id: 2,
          title: "Music CD",
          price: 14.99,
          tax: 10,
          imported: false,
        },
        {
          id: 3,
          title: "Chocolate bar",
          price: 0.85,
          tax: 0,
          imported: false,
        },
        {
          id: 4,
          title: "Imported box of chocolates",
          price: 10.0,
          tax: 0,
          imported: true,
        },
        {
          id: 5,
          title: "Imported bottle of perfume",
          price: 47.5,
          tax: 10,
          imported: true,
        },
        {
          id: 6,
          title: "Imported bottle of perfume",
          price: 27.99,
          tax: 10,
          imported: true,
        },
        {
          id: 7,
          title: "Bottle of perfume",
          price: 18.99,
          tax: 10,
          imported: false,
        },
        {
          id: 8,
          title: "Packet of headache pills",
          price: 9.75,
          tax: 0,
          imported: false,
        },
        {
          id: 9,
          title: "Box of imported chocolates",
          price: 11.25,
          tax: 0,
          imported: true,
        },
      ],
      selectedItem: [],
    };
  },
  methods: {
    PriceWithTax(item) {
      let taxValues = (item.price * item.tax) / 100;

      if (item.imported === true) {
        taxValues = ((item.tax + 5) * item.price) / 100;
      }

      let nearest = 0.05;
      let roundNumber = Math.ceil(taxValues / nearest) * nearest;
      let PriceWithTax = roundNumber.toFixed(2);
      return PriceWithTax;
    },

    PriceWithGross(item) {
      let PriceWithGross = item.price + parseFloat(this.PriceWithTax(item));
      return PriceWithGross.toFixed(2);
    },

    TotalNet(selectedItem) {
      let TotalNet = 0;
      selectedItem.forEach((element) => {
        TotalNet = TotalNet + parseFloat(element.price);
      });

      return TotalNet.toFixed(2);
    },

    TotalTax(selectedItem) {
      let TotalTax = 0;
      selectedItem.forEach((element) => {
        TotalTax = TotalTax + parseFloat(element.PriceWithTax);
      });

      return TotalTax.toFixed(2);
    },
    TotalGross(selectedItem) {
      let TotalGross = 0;
      selectedItem.forEach((element) => {
        TotalGross = TotalGross + parseFloat(element.PriceWithGross);
      });

      return TotalGross.toFixed(2);
    },
    SelectItem(item) {
      item.PriceWithTax = this.PriceWithTax(item);
      item.PriceWithGross = this.PriceWithGross(item);
      this.selectedItem.push(item);
    },
  },

  
};
</script>


<style >
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  padding: 0;
  font-family: sans-serif;
  background: #46529d;
  color: #fff;
}

div h4{
  font-family: 'Times New Roman', Times, serif;
  font-size: 28px;
  text-align: center;
 
}
.text-center {
  text-align: center;
}

.container {
  width: 60%;
  margin: 10% auto;
}

.ListItems {
  background: #fff;
  color: #46529d;
}

.ListItems span {
  display: inline-block;
  text-align: center;
  padding: 10px 0;
  font-size: 20px;
  border: 0.3px solid #ccc;
}
.ListItems span.title {
  background: #2ebaee;
  color: #fff;
}

.ListItems span.product {
  width: 60%;
}

.ListItems span.price {
  width: 20%;
}

.ListItems span.selection {
  width: 20%;
}

.ListSelectedItems {
  background: #fff;
  color: #46529d;
}

.ListSelectedItems span {
  display: inline-block;
  text-align: center;
  padding: 10px 0;
  font-size: 20px;
  border: 0.3px solid #ccc;
}

.ListSelectedItems span.Selectedtitle {
  background: #2ebaee;
  color: #fff;
}

.ListSelectedItems span.productname {
  width: 60%;
}

.ListSelectedItems span.pricevalue {
  width: 15%;
}

.ListSelectedItems span.taxvalue {
  width: 15%;
}

.ListSelectedItems span.grossvalue {
  width: 10%;
}

.Result {
  background: #fff;
  color: #46529d;
}

.Result span.Total{
  width: 60%;
}

.Result span{
   display: inline-block;
  text-align: center;
  padding: 10px 0;
  font-size: 20px;
  border: 0.3px solid #ccc;
}


.Result span.TotalNet{
  width: 15%;
}

.Result span.TotalTax{
  width: 15%;
}

.Result span.TotalGross{
  width: 10%;
}


</style>