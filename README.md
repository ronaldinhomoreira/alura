segue a baixo meu codigo de JavaScript , parea o projeto do challenge do amigo secreto 
alert ('Amigo Secreto');

let amigos = [];
let listaAmigosElement = document.getElementById('listaAmigos');
let amigoInput = document.getElementById('amigo');
let resultadoElement = document.getElementById('resultado');

function adicionarAmigo() {
    let nome = amigoInput.value.trim();

    if (nome === '') {
        alert('Por favor, digite um nome.');
        return;
    }

    amigos.push(nome);
    amigoInput.value = '';
    atualizarListaAmigos();
}

function atualizarListaAmigos() {
    listaAmigosElement.innerHTML = '';
    amigos.forEach(amigo => {
        let li = document.createElement('li');
        li.textContent = amigo;
        listaAmigosElement.appendChild(li);
    });
}

function sortearAmigo() {
    if (amigos.length < 2) {
        alert('Adicione pelo menos dois amigos para o sorteio.');
        return;
    }

    let sorteio = {};
    let amigosDisponiveis = [...amigos];

    amigos.forEach(amigo => {
        let sorteado;
        do {
            let indiceSorteado = Math.floor(Math.random() * amigosDisponiveis.length);
            sorteado = amigosDisponiveis[indiceSorteado]; 
        } while (sorteado === amigo || sorteio[sorteado] === amigo); 

        sorteio[amigo] = sorteado;
        amigosDisponiveis.splice(amigosDisponiveis.indexOf(sorteado), 1); 
    });

    exibirResultado(sorteio);
}

function exibirResultado(sorteio) {
    resultadoElement.innerHTML = '';
    for (let amigo in sorteio) {
        let li = document.createElement('li');
        li.textContent = `${amigo} tirou ${sorteio[amigo]}`;
        resultadoElement.appendChild(li);
    }
}
