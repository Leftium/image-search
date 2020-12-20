<script type='text/coffeescript'>
    queryInput = null

    urlRE = RegExp '^http', 'i'

    handleKeyDown = (e) ->
        console.log 'Key down'
        if e.key is 'Enter'
            e.preventDefault()
            handleClickEverywhere e

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

    handleClickUnsplash = (e) ->
        console.log 'handleClickUnsplash'
        query = queryInput.value.trim()
        window.open "https://unsplash.com/s/photos/#{query}", '_blank'

    handleClickPixabay = (e) ->
        console.log 'handleClickPixabay'
        query = queryInput.value.trim()
        window.open "https://pixabay.com/images/search/#{query}/", '_blank'

    handleClickPexels = (e) ->
        console.log 'handleClickPexels'
        query = queryInput.value.trim()
        window.open "https://www.pexels.com/search/#{query}/", '_blank'

    handleClickStockUnlimited = (e) ->
        console.log 'handleClickStockUnlimited'
        query = queryInput.value.trim()
        window.open "https://www.stockunlimited.com/vector-image/?word=#{query}", '_blank'

    handleClickYayImages = (e) ->
        console.log 'handleClickYayImages'
        query = queryInput.value.trim()
        window.open "https://yayimages.com/search?type=-1&phrase=#{query}", '_blank'


    handleClickEverywhere = (e) ->
        console.log queryInput.value
        query = queryInput.value.trim()

        handleClickGoogleImages(e)
        handleClickYandexImages(e)

        if not urlRE.test query
            console.log 'URL detected'
            handleClickUnsplash(e)
            await setTimeout( (() -> true), 500)
            handleClickPixabay(e)
            await setTimeout( (() -> true), 500)
            handleClickPexels(e)
            await setTimeout( (() -> true), 500)
            handleClickStockUnlimited(e)
            await setTimeout( (() -> true), 500)
            handleClickYayImages(e)
</script>

<template lang=pug>
main
    div: input(bind:this='{queryInput}' on:keydown='{handleKeyDown}')
    div
        button(class='everywhere' on:click='{handleClickEverywhere}') Everywhere!
        button(on:click='{handleClickGoogleImages}') Google Images
        button(on:click='{handleClickYandexImages}') Yandex Images
        button(on:click='{handleClickUnsplash}') Unsplash
        button(on:click='{handleClickPixabay}') Pixabay
        button(on:click='{handleClickPexels}') Pexels
        button(on:click='{handleClickStockUnlimited}') StockUnlimited
        button(on:click='{handleClickYayImages}') YayImages


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

    .everywhere {
        color: white;
        background-color: #268bd2;
        font-weight: bold;
    }

    @media (min-width: 640px) {
        main {
            max-width: none;
        }
    }
</style>
