<style>
    .component-login .container-login {
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
    }
</style>

<script>
    import { onMount } from 'svelte';
    
    let isDesktop,
    hasTouched = { login: false, password: false },
    hasError = { login: '', password: '' },
    inputGroup = { login: '', password: '' },
    isPassword = true;

    onMount(() => { isDesktop = window.innerWidth > 1024 })

    const checkInput = $param_event => {
        console.log("type :: " + $param_event.type);
        let inputName = $param_event.currentTarget.name;
        if(!hasTouched[inputName]) hasTouched[inputName] = true;
        hasError[inputName] = !inputGroup[inputName] ? "Por favor insira seus dados adequadamente." : inputGroup[inputName].length < 3 ? "Por favor, preencha este campo com no mínimo 3 caracteres" : "";
    }
</script>

<section class="component-login">
    <div class="row">
        <div class="column { isDesktop ? 'column-50' : 'column-90' } column-center">
            <div class="container-login">
                <div class="form-login">
                    <h2 class="text-white text-bold text-center">Tu<span class="text-special">Do</span></h2>
                    <div class="row">
                        <div class="column column-90 column-center">
                            <span class="text-white text-bold">Usuário</span>
                            <div class="row">
                                <div class="column column-margin">
                                    <input name="login" class="input-field text-white" on:change="{ checkInput }" bind:value={ inputGroup.login } type="text" placeholder="Insira seu nome de usuário aqui">
                                    { #if hasError.login && hasTouched.login } <span class="text-white"> { hasError.login } </span> { /if }
                                </div>
                            </div>
                            <span class="text-white text-bold">Senha</span>
                            <div class="row">
                                <div class="column column-flex column-margin">
                                    
                                    {#if isPassword}
                                        <input name="password" class="input-field text-white" on:change="{ checkInput }" bind:value={ inputGroup.password } type="password" placeholder="Insira sua senha aqui">
                                    {:else}
                                        <input name="password" class="input-field text-white" on:change="{ checkInput }" bind:value={ inputGroup.password } type="text" placeholder="Insira sua senha aqui">
                                    {/if}

                                    <span on:click="{() => { isPassword = !isPassword }}" class="text-white icon fas { isPassword ? 'fa-eye-slash' :  'fa-eye' }"></span>
                                </div>
                            </div>
                            { #if hasError.password && hasTouched.password }
                                <div class="row">
                                    <div class="column">
                                        <p class="text-white"> { hasError.password } </p>
                                    </div>
                                </div>
                            { /if }
                            <div class="row">
                                <div class="column text-center">
                                    <a class="button button-primary { !inputGroup.password || !inputGroup.login || hasError.login || hasError.password ? 'button-disabled' : '' }"><span class="fas fa-sign-in-alt"></span> entrar</a>
                                </div>
                            </div>
                            <div class="row">
                                <div class="column">
                                    <span class="text-white">OBS:. Caso seu usuário não exista, o mesmo criado automaticamente.</span>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</section>