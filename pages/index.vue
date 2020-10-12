<template>
    <div class="outline-grid--no-sidebar">
        <header class="outline-grid__header">
            <div class="outline-grid__header__line">
                <span class="outline-grid__header__logo">💡</span>
                <span class="outline-grid__header__search">
                    <input type="text" class="outline-grid__header__search__input" placeholder="Encontre ideias de aplicativos">
                    <span class="outline-grid__header__search__icon">🔎</span>
                </span>
                <button role="button" tabindex="1" class="button--primary">Doar minha ideia</button>
            </div>
            <div class="outline-grid__header__line">
                <button role="button" tabindex="1" class="button--small">Complexidade</button>
                <button role="button" tabindex="1" class="button--small">Plataforma</button>
                <button role="button" tabindex="1" class="button--small">Tags</button>
                <span role="button" tabindex="1" class="button--small--invisible p-margin-left-auto">Recentes primeiro</span>
            </div>
        </header>
        <div class="outline-grid__content">
            <amp-state
                    id="allIdeas"
                    src="https://raw.githubusercontent.com/ideias-de-aplicativos/api/gh-pages/1/ideias.json">
            </amp-state>
            <amp-list
                    width="auto"
                    height="100"
                    layout="fixed-height"
                    src="https://raw.githubusercontent.com/ideias-de-aplicativos/api/gh-pages/1/ideias.json"
                    [src]="filteredIdeas"
                    items="ideas"
                    binding="no"
            >
                <div placeholder>
                    <div class="idea-card-list">
                        <div class="idea-card" v-for="index in 8" :key="index">
                            <h2 class="idea-card__title">Carregando</h2>
                        </div>
                    </div>
                </div>
                <amp-mustache>
                    <template v-pre>
                        <div class="idea-card">
                            <h2 class="idea-card__title">{{title}}</h2>
                            <p class="idea-card__subtitle">{{subtitle}}</p>
                        </div>
                    </template>
                </amp-mustache>
            </amp-list>
        </div>
    </div>
</template>

<style lang="sass">
@import '../sass/0 -helpers/breakpoints'
@import '../sass/0 -helpers/mixins/background-stripes'
@import '../sass/2 - layout/outline-grid'

$card-background__blue: #5cc4bd
$card-background__pink: #f46d85
$card-background__yellow: #ece133
$card-background__orange: #ff8b2e
$card-background__baby-pink: #f395b3
$card-background__green: #77bb63
$card-background__baby-yellow: #fef4bf

.p-margin-left-auto
    margin-left: auto

.button
    display: inline-block
    background-color: #fff
    border: 1px solid #edeae7
    font-size: 14px
    padding: 5px 10px
    line-height: 40px
    border-radius: 4px
    margin-right: spacing(1)
    cursor: pointer

    +modifier("small")
        line-height: 20px
        font-size: 12px

        +modifier("invisible")
            background-color: transparent
            border: 0

    +modifier("primary")
        background-color: $card-background__pink
        color: #fff
        border: 1px solid $card-background__pink

body:before
    content: ""
    display: block
    height: 3px
    @include background-stripes(to right, $card-background__blue, $card-background__pink, $card-background__yellow, $card-background__orange, $card-background__baby-pink, $card-background__green, $card-background__baby-yellow)

amp-list [role='list'],
.idea-card-list
    margin: 0 0 spacing(1) 0
    display: grid
    padding: 0 spacing(1)
    grid-gap: spacing(3)
    grid-template-columns: 100%

    @media(min-width: $screen-tablet-min)
        padding: 0
        grid-gap: spacing(2)
        grid-template-columns: repeat(3, minmax(260px, 1fr))

    @media(min-width: $screen-desktop-min)
        padding: 0
        grid-gap: spacing(2)
        grid-template-columns: repeat(4, minmax(220px, 1fr))

.title
    color: #333

    +modifier("is-1")
        font-size: 32px

    +modifier("is-2")
        font-size: 16px
        line-height: 1.5
        color: #727885
        font-weight: 400

.idea-card
    font-family: sans-serif
    height: 260px
    display: flex
    flex-direction: column
    padding: spacing(2)
    color: #1a181b
    cursor: pointer
    box-shadow: 1px 2px hsl(0, 0, 85%)

    &:nth-child(7n)
        background-color: $card_background__blue

    &:nth-child(7n+1)
        background-color: $card_background__pink

    &:nth-child(7n+2)
        background-color: $card_background__yellow

    &:nth-child(7n+3)
        background-color: $card_background__orange

    &:nth-child(7n+4)
        background-color: $card_background__baby-pink

    &:nth-child(7n+5)
        background-color: $card_background__green

    &:nth-child(7n+6)
        background-color: $card_background__baby-yellow

    +element('title')
        line-height: 1.6

    +element('subtitle')
        line-height: 1.6
        max-height: 100%
        overflow: hidden

</style>

<script>
export default {
    amp: 'only',
    ampLayout: 'default.amp',
    head() {
        return {
            title: 'Ideias de aplicativos',
            meta: [{
                hid: 'description',
                name: 'description',
                content: 'Ideias de aplicativos, websites e projetos. Encontre ideias para aplicativos gratuitas e separadas por categorias, também ideias para trabalhos acadêmicos, tcc, tg e software livre.'
            }],
            link: [{
                hid: 'canonical',
                rel: 'canonical',
                href: 'https://ideias.dev.br/'
            }]
        }
    }
}
</script>
