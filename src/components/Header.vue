<template>
    <div>
        <b-navbar type="dark" variant="dark">
          <b-navbar-nav>
            <!-- <b-nav-item href="#">Home</b-nav-item> -->

                    <!-- Navbar dropdowns -->
            <b-nav-item active><b>Fancy Quiz App</b></b-nav-item>
            
            <b-nav-text>Counter: {{numCorrect}} / {{numTotal}}</b-nav-text>

                    
          </b-navbar-nav>
        </b-navbar>
    </div>
</template>

<script>
export default {
  props:[
    'numCorrect',
    'numTotal'
  ]
}
</script>