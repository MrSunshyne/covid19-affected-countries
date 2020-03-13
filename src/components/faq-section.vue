<template>
    <div class="py-10 container mx-auto">
        <h2 class="text-2xl text-center">FAQ</h2>
        <ul
                class="faq px-8 sm:px-0 grid py-10 grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-10"
        >
            <li>
                <label>What is the source ?</label>
                <p>
                    The list of affected countries are from
                    <a
                            href="https://www.cdc.gov/coronavirus/2019-ncov/locations-confirmed-cases.html"
                    >CDC.gov</a
                    >.
                </p>
            </li>
            <li>
                <label>When was this page last updated?</label>
                <p>Last updated: {{ lastUpdated }}</p>
            </li>
            <li>
                <label>Should I trust this page?</label>
                <p>
                    Please use the
                    <a
                            href="https://www.cdc.gov/coronavirus/2019-ncov/locations-confirmed-cases.html"
                    >official list</a
                    >
                    from CDC to cross check.
                </p>
            </li>
            <li>
                <label>Is this updated automatically?</label>
                <p>
                    No. I update the list whenever practically possible. Anyone can
                    submit a PR to update the list
                    <a href="https://github.com/MrSunshyne/covid19-affected-countries"
                    >here</a
                    >.
                </p>
            </li>
            <li>
                <label
                >I'm a developer, how can I get the list of affected
                    countries?</label
                >
                <p>
                    I haven't found an endpoint for that yet. For now use
                    <a
                            href="https://gist.github.com/MrSunshyne/ee206dedf5b0cfe4303d5320b10fc15f"
                    >this gist</a
                    >
                    to quickly extract the list of countries.
                </p>
            </li>
            <li>
                <label>Why did you build this?</label>
                <p>It's hard to compare by starring at the CDC list of countries.</p>
            </li>
        </ul>
    </div>
</template>

<script>
    export default {
        props: ['lastUpdated']
    }
</script>