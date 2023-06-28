<template>
<div class="col-sm-12 col-md-6 col-lg-4 col-xl-3 d-flex flex-column justify-content-around p-4 bg-white content-box m-4 border rounded shadow-sm box-content">
    <div>
        <h2 class="text-center">Matching Numbers</h2>
        <hr class="m-0 p-0" />
        <div>
            <div class="my-4 p-2 text-md mx-4 border border-2 border-secondary d-flex align-items-center justify-content-center rounded ">
                <span v-if="array.length > 0">{{ array.join(", ") }}</span>
                <span v-else class="info-text">
                    Click on Create New Array button</span>
            </div>
            <div class="d-flex flex-column align-items-center">
                <button type="button" class="btn btn-primary mb-2 py-2 w-75" @click="generateArray">
                    Create New Array
                </button>
                <button type="button" class="btn btn btn-outline-primary mb-2 py-2 w-75" @click="findCombinations">
                    Find Combinations
                </button>
            </div>
        </div>
    </div>

    <div class="mt-3 combi-section">
        <p class="fs-5">Combinations:</p>
        <div v-if="combinations.length > 0 && showCombinations">
            <ul>
                <li v-for="int in combinations" :key="int">
                    {{ int.join(" & ") }}
                    <!--As each int is an array, the join function converts it into a string by seperating it with the "&" seperator-->
                </li>
            </ul>
        </div>
    </div>
    <p v-if="array.length === 0" class="text-info text-center">
        No array or combinations available
    </p>
    <!--I added the showCombinations so as to not show the combinations for the old array and prompt the user to click on the combination button to  view the new combiantions -->
    <span v-else-if="!showCombinations && array.length > 0" class="text-info text-center">
        Click on the Find Combinations button to view combination of 21 for this array</span>
    <span v-else-if="array.length > 0 && combinations.length === 0" class="text-info text-center">There were no combinations of 21 for this array
    </span>
</div>
</template>

<script>
export default {
    name: "CombinationSum",
    data() {
        return {
            array: [],
            combinations: [],
            showCombinations: false, //created to conditionally render the combinations as explained on line 37
        };
    },
    methods: {
        generateArray() {
            this.array = [];
            /*
                  for (let i = 0; i < 10; i++) { // create a random array of 10 integers
                           let randomNumber = Math.floor(Math.random() * 20) + 1;
                         this.array.push(randomNumber); // randoms integers should be between 1 and 20
                        }*/
            /*
                  I decided to have 10 array elements, with no duplicates. If I did the for loop as commented out
                   above, it created less elements, when there were duplicates.
                  So after doing some research,I did a while loop which will continue to push the elements (after checking for duplicates)
                  in the array until there are 10 elements in it*/

            while (this.array.length < 10) {
                const randomInteger = Math.floor(Math.random() * 20) + 1;
                if (this.array.indexOf(randomInteger) === -1) {
                    // This line checks for duplicates. If the random integer does not exist already (if its poistion is -1) in the array, then it will push it to the array. I explored the new Set methos for this. But this I felt was more readable
                    this.array.push(randomInteger);
                }
            }
            this.showCombinations = false;
        },
        findCombinations() {
            this.combinations = [];
            //Before this solution I opted fo the nested loop, but it did not meet the performant criteria (considering we were dealing with a huge number of elements). There were other solutions which included .find methods which after researching I found out that they were less performant
            for (let i = 0; i < this.array.length; i++) {
                const num1 = this.array[i]; //The 1st num you want to compare
                const num2 = 21 - num1; // Here I substract the num1 for 21 to get the other num that I can look up for the array (as the total of these two numbers make 21)
                const indexOfNum2 = this.array.indexOf(num2) //Here I am looking of the index of the num2
                if (this.array.includes(num2) && indexOfNum2 > i) { //This condition will execute when the array includes num2 & and index of num 2 > then the index of the current index. This makes sure you dont get duplicate combinations F.ex 2 &10 and 10 & 2
                    this.combinations.push([i + 1, indexOfNum2 + 1]); // Pushed an array as we require combinations and it will be easy to use later as done in line 28
                }
            }
            this.showCombinations = true;
        },
    },
};
</script>
