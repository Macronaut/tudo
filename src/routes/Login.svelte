<style>
    /* .component-login .container-login {
        -webkit-box-shadow: 0px 0px 5px 0px rgba(0,0,0,0.25);
        -moz-box-shadow: 0px 0px 5px 0px rgba(0,0,0,0.25);
        box-shadow: 0px 0px 5px 0px rgba(0,0,0,0.25);

        background-color: #af0404;
        box-sizing: border-box;
        border-radius: 5px;
        padding: 20px;
    }

    .component-login .container-login .text-special { color: #ff0000 }
    .component-login .row .column .input-field { margin-bottom: 0 }
    .component-login .row .column.column-margin { margin: 10px 0 }    

    .component-login .row .column.column-flex {
        justify-content: space-around;
        align-items: center;
        display: flex;
    }

    .component-login .row .column.column-flex .icon {
        text-align: center;
        cursor: pointer;
        margin: 0 10px;
        width: 27px;
    } */
</style>

<script>
    import { fade } from 'svelte/transition';
    import { onMount } from 'svelte';
    
    let isDesktop,
    hasTouched = { login: false, password: false },
    inputGroup = { login: '', password: '' },
    hasError = { login: '', password: '' },
    isPassword = true;

    onMount(() => { isDesktop = window.innerWidth > 1024 })

    const checkInput = $param_event => {
        console.log("param_event :: " + $param_event.type);
        let inputName = $param_event.currentTarget.name;
        if(!hasTouched[inputName] && $param_event.type === "change") hasTouched[inputName] = true;
        hasError[inputName] = !inputGroup[inputName] ? "* Dado obrigatório" : inputGroup[inputName].length < 3 ? "* Mínimo de 3 caracteres" : "";
    }

    const checkLogin = $param_event => {
        const Account = Parse.Object.extend('Account');
        const query = new Parse.Query(Account);
        
        query.find().then((results) => {
        // You can use the "get" method to get the value of an attribute
        // Ex: response.get("<ATTRIBUTE_NAME>")
        if (typeof document !== 'undefined') document.write(`Account found: ${JSON.stringify(results)}`);
        console.log('Account found', results);
        }, (error) => {
        if (typeof document !== 'undefined') document.write(`Error while fetching Account: ${JSON.stringify(error)}`);
        console.error('Error while fetching Account', error);
        });
    }

    const checkSignup = $param_event => {

    }
</script>

<section class="component-login">
    <!-- <div class="row">
        <div class="column { isDesktop ? 'column-50' : 'column-90' } column-center">
            <div class="container-login">
                <div class="form-login">
                    <h2 class="text-white text-bold text-center">Tu<span class="text-special">Do</span></h2>
                    <div class="row">
                        <div class="column column-90 column-center">
                            <span class="text-white text-bold">Usuário</span>
                            <div class="row">
                                <div class="column column-margin">
                                    <input name="login" class="input-field text-white" on:keyup="{ checkInput }" on:change="{ checkInput }" bind:value={ inputGroup.login } type="text" placeholder="Nome de usuário">
                                </div>
                            </div>
                            
                            { #if hasError.login && hasTouched.login }
                                <div class="row" transition:fade>
                                    <div class="column">
                                        <span class="text-white text-shadow"> { hasError.login } </span>
                                    </div>
                                </div>
                            { /if }

                            <span class="text-white text-bold">Senha</span>
                            <div class="row">
                                <div class="column column-flex column-margin">
                                    
                                    {#if isPassword}
                                        <input name="password" class="input-field text-white" on:keyup="{ checkInput }" on:change="{ checkInput }" bind:value={ inputGroup.password } type="password" placeholder="Senha">
                                    {:else}
                                        <input name="password" class="input-field text-white" on:keyup="{ checkInput }" on:change="{ checkInput }" bind:value={ inputGroup.password } type="text" placeholder="Senha">
                                    {/if}

                                    <span on:click="{() => { isPassword = !isPassword }}" class="text-white icon fas { isPassword ? 'fa-eye-slash' :  'fa-eye' }"></span>
                                </div>
                            </div>
                            
                            { #if hasError.password && hasTouched.password }
                                <div class="row" transition:fade>
                                    <div class="column">
                                        <span class="text-white text-shadow"> { hasError.password } </span>
                                    </div>
                                </div>
                            { /if }
                            
                            <div class="row">
                                <div class="column text-center">
                                    <a on:click={ checkLogin } class="button button-primary { !inputGroup.password || !inputGroup.login || hasError.login || hasError.password ? 'button-disabled' : '' }"><span class="fas fa-sign-in-alt"></span> entrar</a>
                                    <a on:click={ checkSignup } class="button button-secondary { !inputGroup.password || !inputGroup.login || hasError.login || hasError.password ? 'button-disabled' : '' }"><span class="fas fa-user-plus"></span> criar</a>
                                </div>
                            </div>
                            <div class="row">
                                <div class="column">
                                    <span class="text-white">OBS:. Caso seu usuário não exista, o mesmo será criado automaticamente.</span>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div> -->    
    <div class="columns is-centered is-mobile">
        <div class="column is-7-desktop is-11-mobile">
            <div class="box">
                
                <div class="columns is-centered is-mobile">
                    <div class="column">
                        <p class="is-size-2 has-text-centered has-text-weight-bold">Tu<span class="has-text-danger">Do</span></p>
                    </div>                
                </div>

                <div class="columns is-centered is-mobile">
                    <div class="column is-11">

                        <div class="columns is-centered">
                            <div class="column is-8-desktop">
                                <div class="field">                                
                                    <p class="control has-icons-left has-icons-right">
                                        <input on:keyup="{ checkInput }" on:change="{ checkInput }" class="input" type="text" placeholder="Usuário" bind:value={ inputGroup.login }>
                                        <span class="icon is-small is-left"><i class="fas fa-envelope"></i></span>
                                    </p>
                                </div>
                                { #if hasError.login && hasTouched.login } <p class="has-text-danger"> { hasError.login } </p> {/if}
                                <div class="field">                                
                                    <p class="control has-icons-left">
                                        <input on:keyup="{ checkInput }" on:change="{ checkInput }" class="input" type="password" placeholder="Senha" bind:value={ inputGroup.password }>
                                        <span class="icon is-small is-left"><i class="fas fa-lock"></i></span>
                                    </p>
                                </div>
                                { #if hasError.password && hasTouched.password } <p class="has-text-danger"> { hasError.password } </p> {/if}
                                <div class="field">
                                    <p class="control has-text-centered">
                                        { #if !inputGroup.password || !inputGroup.login || hasError.login || hasError.password }
                                            <a class="button is-success" disabled>
                                                <span>Login</span>
                                                <span class="icon is-small"><i class="fas fa-sign-in-alt"></i></span>
                                            </a>
                                            <a class="button is-link" disabled>
                                                <span>Criar</span>
                                                <span class="icon is-small"><i class="fas fa-user-plus"></i></span>
                                            </a>
                                        { :else }
                                            <a class="button is-success">
                                                <span>Login</span>
                                                <span class="icon is-small"><i class="fas fa-sign-in-alt"></i></span>
                                            </a>
                                            <a class="button is-link">
                                                <span>Criar</span>
                                                <span class="icon is-small"><i class="fas fa-user-plus"></i></span>
                                            </a>
                                        { /if }                                    
                                    </p>
                                </div>
                            </div>
                        </div>
                        
                        <div class="columns is-centered">
                            <div class="column is-8-desktop has-text-justified">                                
                                <p>Após o preenchimento dos dados, pressione <span class="has-text-weight-bold">Login</span> para entrar em uma conta existente e <span class="has-text-weight-bold">Criar</span> para gerar uma nova.</p>                                
                            </div>
                        </div>

                    </div>
                </div>

            </div>
        </div>        
    </div>
</section>