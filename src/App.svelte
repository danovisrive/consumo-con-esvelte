<script>
  import svelteLogo from './assets/svelte.svg'
  import viteLogo from '/vite.svg'
  import Counter from './lib/Counter.svelte'




const API_URL = 'https://jsonplaceholder.typicode.com';

const xhr = new XMLHttpRequest();

function onRequestHandler() {
  if (this.readyState === 4 && this.status === 200) {
    try {
      const data = JSON.parse(this.response);

      const appElement = document.querySelector('#app');
      if (appElement) {
                const table = document.createElement('table');
        const tableHeader = table.insertRow();


        tableHeader.insertCell().textContent = 'ID';
        tableHeader.insertCell().textContent = 'Name';
        tableHeader.insertCell().textContent = 'Username';
        tableHeader.insertCell().textContent = 'Email';
        tableHeader.insertCell().textContent = 'Address';
        tableHeader.insertCell().textContent = 'Phone';
        tableHeader.insertCell().textContent = 'Website';
        tableHeader.insertCell().textContent = 'Company Name';

        const userData = data.map(user => {
          const row = table.insertRow();
          row.insertCell().textContent = user.id;
          row.insertCell().textContent = user.name;
          row.insertCell().textContent = user.username;
          row.insertCell().textContent = user.email;
          row.insertCell().textContent = `${user.address.street}, ${user.address.city}, ${user.address.zipcode}`; // Concatenated address
          row.insertCell().textContent = user.phone;
          row.insertCell().textContent = user.website;
          row.insertCell().textContent = user.company.name;
          return row;
        });

        appElement.innerHTML = '';
        appElement.appendChild(table);
      } else {
        console.error('Elemento con ID "app" no encontrado para mostrar datos.');
      }
    } catch (error) {
      console.error('Error al analizar la respuesta JSON:', error);
    }
  } else {
    console.error('Solicitud fallida. Estado:', this.status);
  }
}

xhr.addEventListener('load', onRequestHandler);
xhr.open('GET', `${API_URL}/users`);
xhr.send();

</script>