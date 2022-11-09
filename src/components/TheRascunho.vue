<script>

export default {
    methods: {
        getKey(columns) {
            const arr = [],
                obj = Object.keys(columns);
            for (var x in obj) {
                if (columns[obj[x]] == "true") {
                    arr.push(obj[x]);
                }
            }
            return arr;
        },
        getStats(X) {
            const arr = [],
            obj1 = Object.keys(X);
            for (var i in obj1) {
                console.log(obj1[i])
                console.log(X(obj1[i]))
            }
            return arr;
        },
    },
}


</script>