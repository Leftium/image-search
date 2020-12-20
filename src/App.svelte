<script type='text/coffeescript'>
    queryInput = null

    urlRE = RegExp '^http', 'i'

    handleKeyDown = (e) ->
        console.log 'Key down'
        if e.key is 'Enter'
            e.preventDefault()
            handleClickGoogleImages e

    handleClickGoogleImages = (e) ->
        console.log queryInput.value
        query = queryInput.value.trim()

        if urlRE.test query
            console.log 'URL detected'
            window.open "http://images.google.com/searchbyimage?image_url=#{query}", '_blank'
        else
            window.open "https://www.google.com/search?tbm=isch&q=#{query}", '_blank'


    handleClickYandexImages = (e) ->
        console.log queryInput.value
        query = queryInput.value.trim()

        if urlRE.test query
            console.log 'URL detected'
            window.open "https://yandex.com/images/search?rpt=imageview&url=#{query}", '_blank'
        else
            window.open "https://yandex.com/images/search?text=#{query}", '_blank'
</script>

<template lang=pug>
main
    div: input(bind:this='{queryInput}' on:keydown='{handleKeyDown}')
    div
        button(on:click='{handleClickGoogleImages}') Google Images
        button(on:click='{handleClickYandexImages}') Yandex Images


</template>

<style>
    main {
        text-align: center;
        padding: 1em;
        max-width: 240px;
        margin: 0 auto;
    }

    input {
        width: 100%;
    }

    @media (min-width: 640px) {
        main {
            max-width: none;
        }
    }
</style>
