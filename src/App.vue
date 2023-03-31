<script>
export default {
	data() {
		return {
			maxLoad: '',
			curLoad: '',
			curEndurance: '',
			status: 'Your current load status is ',
			isCalculated: false,
			isAdvanced: false,
			checkedItems: [],
		}
	},
	methods: {
		onMax(e) {
			this.maxLoad = e.maxLoad.value,
			this.curLoad = e.curLoad.value
		},
		onAdvanced(e) {
			this.curEndurance = e.curEndurance.value
		},
		toggle() {
			if (!this.isCalculated) {
				this.isCalculated = true;
			} else {
				this.isCalculated = false;
				this.maxLoad = '';
				this.curLoad = '';
				this.curEndurance = '';
			}
		},
		advanced() {
			if (!this.isAdvanced) {
				this.isAdvanced = true;
			} else {
				this.isAdvanced = false;
				this.maxLoad = '';
				this.curLoad = '';
				this.curEndurance = '';
			}
		},
		roundedTo(n, place) {
			return +(Math.round(n + "e+" + place) + "e-" + place)
		},
		btnForward() {
			let audio = new Audio('/er-new.mp3')
			audio.play()
		},
		btnBack() {
			let audio = new Audio('/er-reset.mp3')
			audio.play()
		},
		calcMax(n) {
			let curLoad = 45
			if (n > 8 && n < 13) {
				curLoad += ((n - 8)*1.6)
			} else if (n >= 13 && n < 21) {
				curLoad = 52.9 + ((n - 13)*1.6)
			} else if (n >= 21 && n < 26) {
				curLoad = 65.6 + ((n - 21)*1.6)
			} else if (n >= 26 && n < 29) {
				curLoad = 73 + ((n - 26)*1.1)
			} else if (n == 29) {
				curLoad = 76.4
			} else if (n >= 30 && n < 37) {
				curLoad = 77.6 + ((n - 30)*1.3)
			} else if (n >= 37 && n < 39) {
				curLoad = 86.8 + ((n - 37)*1.3)
			} else if (n >= 39 && n < 46) {
				curLoad = 89.5 + ((n - 39)*1.4)
			} else if (n >= 46 && n < 49) {
				curLoad = 99.4 + ((n - 46)*1.4)
			} else if (n == 49 || n == 50) {
				curLoad = 103.7 + ((n - 49)*1.5)
			} else if (n >= 51 && n < 54) {
				curLoad = 106.6 + ((n - 51)*1.5)
			} else if (n >= 54 && n < 61) {
				curLoad = 111 + ((n - 54)*1.5)
			} else if (n == 61) {
				curLoad = 121
			} else if (n >= 62 && n < 66) {
				curLoad = 122.1 + (n - 62)
			} else if (n >= 66 && n < 70) {
				curLoad = 126.2 + (n - 66)
			} else if (n >= 70 && n < 74) {
				curLoad = 130.3 + (n - 70)
			} else if (n >= 74 && n < 78) {
				curLoad = 134.4 + (n - 74)
			} else if (n >= 78 && n < 82) {
				curLoad = 138.5 + (n - 78)
			} else if (n >= 82 && n < 86) {
				curLoad = 142.6 + (n - 82)
			} else if (n >= 86 && n < 90) {
				curLoad = 146.7 + (n - 86)
			} else if (n >= 90 && n < 94) {
				curLoad = 150.8 + (n - 90)
			} else if (n >= 94 && n < 98) {
				curLoad = 154.9 + (n - 94)
			} else if (n == 98 || n == 99) {
				curLoad = 159 + (n - 98)
			}
			if (this.checkedItems.includes("Arsenal Charm")) {
				curLoad *= 1.15
			}
			if (this.checkedItems.includes("Arsenal Charm +1")) {
				curLoad *= 1.17
			}
			if (this.checkedItems.includes("Great-Jar's Arsenal")) {
				curLoad *= 1.19
			}
			if (this.checkedItems.includes("Erdtree's Favor")) {
				curLoad *= 1.05
			}
			if (this.checkedItems.includes("Erdtree's Favor +1")) {
				curLoad *= 1.065
			}
			if (this.checkedItems.includes("Erdtree's Favor +2")) {
				curLoad *= 1.08
			}
			return curLoad
		},
		clear() {
		this.checkedItems = [];
		},
	}
}
</script>

<template>
	<div class="content">
		<div>
			<img class="logo" src="/er-logo.png">
			<h1>E<h1 class="smaller">LDEN RIN</h1>G</h1>
			<h3>Equip Load Calculator</h3>
		</div>
		<br/>
	</div>
	<div class="content">
		<div v-if="isCalculated==false && isAdvanced==false" class="start">
			<form>
				<input v-model="maxLoad" placeholder="MAX EQUIP LOAD" input type="text" id="max" name="max" required>
				<br/>
				<input v-model="curLoad" placeholder="CURRENT LOAD (optional)" input type="text" id="current" name="current">
				<br/>
				<button @click="toggle(); btnForward()">CALCULATE</button>
			</form>
			<br/>
			<button @click="advanced(); btnForward()">ADVANCED</button>
		</div>
		<div v-if="isCalculated==false && isAdvanced==true" class="start">
			<form>
				<input v-model="curEndurance" placeholder="ENDURANCE" input type="text" id="endurance" name="endurance" required>
				<br/>
				<div class="items">
					<div class="item">
						<input type="checkbox" id="arsenalcharm" value="Arsenal Charm" v-model="checkedItems" class="defaultCheckbox"><label for="arsenalcharm">Arsenal Charm</label>
					</div>
					<div class="item">
						<input type="checkbox" id="arsenalcharm1" value="Arsenal Charm +1" v-model="checkedItems" class="defaultCheckbox"><label for="arsenalcharm1">Arsenal Charm +1</label>
					</div>
					<div class="item">
						<input type="checkbox" id="erdtree" value="Erdtree&#x27;s Favor" v-model="checkedItems" class="defaultCheckbox">
						<label for="erdtree">Erdtree's Favor</label>
					</div>
					<div class="item">
						<input type="checkbox" id="erdtree1" value="Erdtree&#x27;s Favor +1" v-model="checkedItems" class="defaultCheckbox">
						<label for="erdtree1">Erdtree's Favor +1</label>
					</div>
					<div class="item">
						<input type="checkbox" id="erdtree2" value="Erdtree&#x27;s Favor +2" v-model="checkedItems" class="defaultCheckbox">
						<label for="erdtree2">Erdtree's Favor +2</label>
					</div>
					<div class="item">
						<input type="checkbox" id="greatjar" value="Great-Jar&#x27;s Arsenal" v-model="checkedItems" class="defaultCheckbox">
						<label for="greatjar">Great-Jar's Arsenal</label>
					</div>
				</div>
				<br/>
				<button @click="toggle(); btnForward()">CALCULATE</button>
				
			</form>
			<br/>
			<button @click="advanced(); btnBack()">BACK</button>
		</div>
		<div v-if="isCalculated==true && isAdvanced==false" class="results">
			<h4 v-if="maxLoad!='' && curLoad==''">
				Your maximum equip load is {{ maxLoad }}
			</h4>
			<h2 v-if="maxLoad!='' && curLoad!=''">
				{{ curLoad }} / {{ maxLoad }}
			</h2>
			<p v-if="curLoad==''">
				<!-- LEAVE EMPTY -->
			</p>
			<p v-else-if="curLoad<=roundedTo(maxLoad*.2999, 1)">
				{{ status }} LIGHT
			</p>
			<p v-else-if="curLoad>roundedTo(maxLoad*.2999, 1) && curLoad<=roundedTo(maxLoad*.6999, 1)">
				{{ status }} MEDIUM
			</p>
			<p v-else-if="curLoad>roundedTo(maxLoad*.6999, 1) && curLoad<=roundedTo(maxLoad*.9999, 1)">
				{{ status }} HEAVY
			</p>
			<p v-else-if="curLoad>=maxLoad">
				{{ status }} OVERLOADED
			</p>
			<br/>
			<div class="status">
				<p>
					LIGHT up to {{ roundedTo(maxLoad*.299, 1) }}
				</p>
				<p>
					MEDIUM from {{ roundedTo(maxLoad*.3, 1) }} to {{ roundedTo(maxLoad*.699, 1) }}
				</p>
				<p>
					HEAVY from {{ roundedTo(maxLoad*.7, 1) }} to {{ roundedTo(maxLoad*.999, 1) }}
				</p>
			</div>
			<br/>
			<button @click="toggle(); btnBack()">RESET &#8634;</button>
		</div>
		<div v-if="isCalculated==true && isAdvanced==true" class="results">
			<h4 v-if="curEndurance!=''">
				Your current endurance is {{ curEndurance }}
			</h4>
			<h4 v-if="curEndurance!=''">
				Your maximum equip load is {{ roundedTo(calcMax(curEndurance), 1) }}
			</h4>
			<h4 v-if="checkedItems[0]">
				<br/>
				Equipped items:
			</h4>
			<li v-for="item in checkedItems">
				{{ item }}
			</li>
			<br/>
			<div class="status">
				<p>
					LIGHT up to {{ roundedTo(calcMax(curEndurance)*.2999, 1) }}
				</p>
				<p>
					MEDIUM from {{ roundedTo(calcMax(curEndurance)*.3, 1) }} to {{ roundedTo(calcMax(curEndurance)*.6999, 1) }}
				</p>
				<p>
					HEAVY from {{ roundedTo(calcMax(curEndurance)*.7, 1) }} to {{ roundedTo(calcMax(curEndurance)*.9999, 1) }}
				</p>
			</div>
			<br/>
			<button @click="toggle(); clear(); btnBack()">RESET &#8634;</button>
		</div>
		
	</div>
</template>

<style>
.logo {
    max-width: 300px;
  }
h1 {
	color: rgb(240, 224, 145);
	font-family: mantinia-regular;
	display: flex;
    align-items: center;
    justify-content: center;
	font-size: 3rem;
	text-shadow: 0px 0px 20px rgba(0,0,0,1);
}
.smaller {
	font-size: 2.3rem;
}
h2 {
	display: flex;
    align-items: center;
    justify-content: center;
}
h3 {
	display: flex;
    align-items: center;
    justify-content: center;
	font-family: crimson-roman;
	font-size: x-large;
	text-shadow: 0px 0px 8px rgba(0,0,0,.8);
}
.content {
	display: flex;
	flex-direction: column;
    align-items: center;
    justify-content: center;
	font-family: crimson-roman;
	font-size: 1.1rem;
}
.start {
	display: flex;
	flex-direction: column;
    align-items: center;
    justify-content: center;
}
.items {
	text-align: left;
	display: flex;
	flex-direction: row;
	flex-wrap: wrap;
	width: 250px;
}
.item:nth-child(2n) {
	flex-basis: 100%;
}
.advanced {
	display: flex;
	flex-direction: column;
    align-items: center;
    justify-content: center;
}
.results {
	display: flex;
	flex-direction: column;
    align-items: center;
    justify-content: center;
}
li {
	font-size: medium;
}
input {
	font-family: crimson-roman;
	font-size: large;
	align-content: center;
	padding-left: .5rem;
	padding-right: .5rem;
	text-align: center;
	width: 300px;
	background-color: rgb(12, 12, 12);
	color: white;
	border-style: hidden;
}
input.defaultCheckbox {
	width: 20px !important;
	margin-left: 10px;
	margin-right: 10px;
}
form {
	display: flex;
	flex-direction: column;
	align-items: center;
    justify-content: center;
}
button {
	font-family: crimson-roman;
	font-size: large;
	width: 200px;
	padding: 0px;
	background-color: rgb(12, 12, 12);
	border:solid white 1px;
	color: rgb(187, 187, 187);
}
button:hover{
	background-color: rgb(26, 26, 26);
	cursor: pointer;
	box-shadow: 0px 0px 5px 0px rgba(255,255,255,0.25);
}
</style>