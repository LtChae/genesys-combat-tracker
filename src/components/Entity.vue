<template>
  <div class="wrapper" v-bind:class="{dead: isDead}">
    <div class="identity-wrapper">
      <div class="stat-row">
        <input v-model="name" class="input-wide" placeholder="unnamed goon" />
      </div>
      <div class="stat-row">
        <div>
          <input type="radio" id="minion" value="minion" v-model="type" />
          <label for="minion">
            <img class="icon" src="../assets/backup.png" title="Minion" />
          </label>
        </div>
        <div>
          <input type="radio" id="rival" value="rival" v-model="type" />
          <label for="rival">
            <img class="icon" src="../assets/person.png" title="Rival" />
          </label>
        </div>
        <div>
          <input type="radio" id="nemesis" value="nemesis" v-model="type" />
          <label for="nemesis">
            <img class="icon" src="../assets/strong.png" title="Nemesis" />
          </label>
        </div>
      </div>
    </div>
    <div class="stats-wrapper">
      <div class="stat-row">
        <img class="icon" src="../assets/breastplate.png" title="Soak" />
        <input v-model="soak" class="input-small" />
        <img class="icon" src="../assets/swords-emblem.png" title="Melee Defense" />
        <input v-model="meleeDefense" class="input-small" />
        <img class="icon" src="../assets/arrows-shield.png" title="Ranged Defense" />
        <input v-model="rangedDefense" class="input-small" />
      </div>
      <div class="stat-row" v-if="type == 'minion'">
        <div>
          <img class="icon" src="../assets/backup.png" title="Number of Minions" />
          <input v-model="quantity" class="input-small" />
        </div>
        <div>
          <img
            class="icon"
            src="../assets/health-per-minion.png"
            title="Wound Threshold per Minion"
          />
          <input v-model="woundThreshold" class="input-small" />
        </div>
      </div>
      <div class="stat-row">
        <div>
          <img class="icon" src="../assets/heart-drop.png" title="Wounds out of Wound Threshold" />
          <input v-model="wounds" class="input-small" />
          <span>/</span>
          <input v-model="woundThreshold" class="input-small" v-if="type != 'minion'" />
          <input v-model="minionThreshold" class="input-small" v-if="type == 'minion'" disabled />
        </div>
      </div>
      <div class="stat-row" v-if="type == 'nemesis'">
        <div>
          <img class="icon" src="../assets/beams-aura.png" title="Strain out of Strain Threshold" />
          <input v-model="strain" class="input-small" />
          <span>/</span>
          <input v-model="strainThreshold" class="input-small" />
        </div>
      </div>
    </div>
    <div class="notes-wrapper" v-if="notesExpanded">
      <textarea v-model="notes"></textarea>
    </div>
    <div class="actions-wrapper">
      <div class="stat-row">
        <img class="action" src="../assets/notes.png" v-on:click="notesExpanded = !notesExpanded" title="Notes" />
        <img class="action" src="../assets/duplicate.png" title="Duplicate" />
        <img class="action" src="../assets/trash-can.png" title="Delete" />
      </div>
    </div>
    
  </div>
</template>

<script>
export default {
  name: "Entity",
  props: {},
  data: () => {
    return {
      name: "",
      soak: 0,
      wounds: 0,
      woundThreshold: 0,
      strain: 0,
      strainThreshold: 0,
      type: "nemesis",
      quantity: 0,
      meleeDefense: 0,
      rangedDefense: 0,
      notes: "",
      notesExpanded: false
    };
  },
  computed: {
    minionThreshold: function() {
      return this.quantity * this.woundThreshold;
    },
    isDead: function() {
      if (this.type == "minion") {
        return this.wounds > this.minionThreshold;
      } else if (this.type == "nemesis") {
        return (
          this.wounds > this.woundThreshold ||
          this.strain > this.strainThreshold
        );
      } else {
        return this.wounds > this.woundThreshold;
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.input-wide {
  width: 90%;
}
.input-small {
  width: 1.5rem;
}
.stat-row {
  width: 100%;
  display: flex;
  justify-content: space-around;
}
.icon {
  height: 1rem;
  vertical-align: middle;
}
.stats-wrapper {
  display: inline-flex;
  flex-wrap: wrap;
  justify-content: space-between;

  border-top: 1px solid black;
    padding: 5px;
}

.wrapper {
  border: 2px solid black;
  width: 10rem;
}

.identity-wrapper {
  display: inline-flex;
  flex-wrap: wrap;
  justify-content: space-between;
}

.dead {
  border: 2px solid crimson;
}

.dead2:after {
  content: " ";
  display: block;
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  z-index: -11;
  opacity: 0.6;
}

textarea {
  width: 100%;
  height: 3rem;
  -webkit-box-sizing: border-box; /* Safari/Chrome, other WebKit */
  -moz-box-sizing: border-box; /* Firefox, other Gecko */
  box-sizing: border-box; /* Opera/IE 8+ */
}

.actions-wrapper {
 border-top: 1px solid black
}

.action {
  border-radius: 50%;
  border: 1px solid white;
  width: 1.25rem;
  height: 1.25rem;
  padding: 5px;
  vertical-align: middle;
}
</style>
