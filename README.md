<!-- @format -->

# Route Exercise FER Wave 16

### 1. Apa perbedaan utama antara React Router v5 dan v6?

| Perbedaan             | React Router v5                                                 | React Router v6                                           |
| --------------------- | --------------------------------------------------------------- | --------------------------------------------------------- |
| Component untuk Route | Menggunakan `<Route>` dan <Switch>                              | Menggunakan `<Routes>` dan `<Route>`                      |
| Penggunaan Router     | Terdapat beberapa tipe router (BrowserRouter, HashRouter, etc.) | Hanya menggunakan `<BrowserRouter>` atau `<MemoryRouter>` |
| Penanganan Redirect   | Menggunakan `<Redirect>` komponen atau fungsi `history.push`    | Menggunakan fungsi navigate dari hook `useNavigate`       |
| Penanganan 404        | Penggunaan <Route> dengan path="\*"                             | Menggunakan rute terakhir dalam <Routes>                  |
| Nesting Route         | Menggunakan rute bersarang dalam komponen `<Route>`             | Menggunakan rute bersarang dalam komponen `<Routes>`      |

### 2. Apa fungsi dari komponen `<Routes>` di React Router v6?

`<Routes>` dalam React Router v6 berfungsi untuk menampung semua rute (routes) yang kita perlukan dalam pembentukan aplikasi.

contoh:

```js
<Routes>
     <Route path=""/"" element={<Home />} />
     <Route path=""/about"" element={<About />} />
     <Route path=""/contact"" element={<Contact />} />
</Routes>"
```

### 3. Bagaimana cara mendefinisikan rute dasar di React Router v6?

dengan path kosong ("")

```js
import { BrowserRouter as Router, Routes, Route } from 'react-router-dom';

const Home = () => <h1>Selamat datang di Halaman Beranda!</h1>;

const App = () => {
  return (
    <Router>
      <Routes>
        {/* Rute dasar */}
        <Route path="" element={<Home />} />

        {/* Rute lainnya */}
        {/* ... */}
      </Routes>
    </Router>
  );
};

export default App;
```

Dalam contoh ini, `<Route path="" element={<Home />} />` menentukan rute dasar yang akan ditampilkan saat aplikasi dimuat. Ketika URL aplikasi berada di root (misalnya "http://localhost:3000/"), komponen `<Home />` akan ditampilkan.

### 4. Apa itu nested routes di React Router v6 dan bagaimana cara menerapkannya?

Nested routes di React Router v6 adalah konsep di mana kita dapat menempatkan satu set rute di dalam rute lainnya. Ini berguna ketika kita memiliki struktur halaman yang terdiri dari beberapa komponen yang saling berhubungan secara
hierarkis.

Misal kita punya page about, di page about tersebut terdiri dari beberapa section atau bagian. jadi di routenya tetap dimulai dari about/{namaSection}

```js
import { BrowserRouter as Router, Routes, Route, Link } from 'react-router-dom';

const Home = () => <h1>Selamat datang di Halaman Beranda!</h1>;
const About = () => <h1>Ini adalah Halaman Tentang Kami.</h1>;
const Contact = () => <h1>Hubungi Kami di Halaman Kontak.</h1>;

const App = () => {
  return (
    <Router>
      <div>
        <nav>
          <ul>
            <li>
              <Link to="/">Beranda</Link>
            </li>
            <li>
              <Link to="/about">Tentang Kami</Link>
            </li>
            <li>
              <Link to="/contact">Kontak</Link>
            </li>
          </ul>
        </nav>

        <Routes>
          <Route path="/" element={<Home />} />
          <Route path="/about" element={<About />} />
          <Route path="/contact" element={<Contact />} />
        </Routes>
      </div>
    </Router>
  );
};

export default App;
```

```js
const About = () => {
  return (
    <div>
      <h1>About</h1>
      <nav>
        <ul>
          <li>
            <Link to="/about/history">History</Link>
          </li>
          <li>
            <Link to="/about/team">Our Team</Link>
          </li>
          <li>
            <Link to="/about/location">Location</Link>
          </li>
        </ul>
      </nav>
      <Routes>
        <Route path="history" element={<History />} />
        <Route path="team" element={<Team />} />
        <Route path="location" element={<Location />} />
      </Routes>
    </div>
  );
};
```

### 5. Apa fungsi dari hook useNavigate di React Router v6?

hook useNavigate untuk mendapatkan fungsi navigate. Ketika tombol diklik, fungsi navigate akan dipanggil dengan rute yang dituju sebagai argumen, dalam hal ini "/about". Ini akan mengarahkan pengguna ke halaman "/about".

```js
const MyComponent = () => {
  const navigate = useNavigate();
  const handleClick = () => {
    // Navigasi ke halaman "/about" ketika tombol diklik
    navigate('/about');
  };

  return (
    <div>
      <h1>Halaman Utama</h1>
      <button onClick={handleClick}>About</button>
    </div>
  );
};
```

### 6. Bagaimana cara melakukan redirect di React Router v6?

Untuk melakukan redirect di React Router v6, kita dapat menggunakan fungsi navigate dari hook useNavigate.

### 7. Apa kegunaan dari useParams hook dalam React Router v6?

useParams adalah hook yang disediakan oleh React Router v6 yang memungkinkan kita untuk mengakses parameter yang dikirimkan melalui URL

```js
<Route path="/users/:id" element={<UserProfile />} />
```

```js
import { useParams } from 'react-router-dom';

const UserProfile = () => {
  // Menggunakan useParams untuk mengambil nilai parameter ":id" dari URL
  const { id } = useParams();

  return (
    <div>
      <h1>Profil Pengguna</h1>
      <p>ID Pengguna: {id}</p>
    </div>
  );
};
```

Dalam contoh di atas, kita menggunakan useParams untuk mengambil nilai parameter ":id" dari URL. Nilai parameter tersebut kemudian digunakan untuk menampilkan ID pengguna di dalam komponen UserProfile.

### 8. Bagaimana cara mengakses query string di React Router v6?

useSearchParams. Hook ini memungkinkan kita untuk mendapatkan nilai dari query string yang terdapat pada URL.

### 9. Apa itu outlet di React Router v6 dan bagaimana penggunaannya?

Outlet dalam React Router v6 adalah sebuah komponen yang digunakan untuk menampilkan konten dari rute yang ditentukan. Ketika kita menggunakan outlet, React Router akan menempatkan konten dari rute yang sesuai di tempat di mana outlet
tersebut ditempatkan dalam aplikasi kita.

Contohnya, jika kita memiliki rute seperti ini:

```js
<Routes>
  <Route path="/" element={<Home />} />
  <Route path="/about" element={<About />} />
  <Route path="/contact" element={<Contact />} />
</Routes>
```

Kita dapat menempatkan outlet di komponen utama kita, yang akan menampilkan konten dari rute yang sesuai:

```js
function App() {
  return (
    <div>
      <h1>My App</h1>
      {/* Outlet akan menampilkan konten dari rute yang sesuai */}
      <Outlet />
    </div>
  );
}
```

Dalam contoh di atas, jika kita menavigasi ke /about, maka komponen `<About />` akan ditampilkan di dalam outlet. Jadi, outlet memungkinkan kita untuk menentukan di mana konten dari rute-rute aplikasi kita akan ditampilkan.

### 10. Bagaimana cara melindungi rute yang memerlukan autentikasi di React Router v6?

hal tersebut dapat dilakukan dengan meembuat komponen `PrivateRoute` yang akan memeriksa status autentikasi pengguna.

```js
import { Navigate, Route } from 'react-router-dom';

const PrivateRoute = ({ isAuthenticated, ...props }) => {
  if (isAuthenticated) {
    // Jika pengguna terautentikasi, izinkan akses ke rute yang dituju
    return <Route {...props} />;
  } else {
    // Jika pengguna tidak terautentikasi, arahkan ke halaman login
    return <Navigate to="/login" />;
  }
};
```

kemudian komponen tersebut digunakan di dalam route, kemudian gunakan prop `isAuthenticated` yang menunjukkan apakah pengguna sudah terautentikasi atau belum.

```js
<Routes>
  <Route path="/login" element={<LoginPage />} />
  <PrivateRoute path="/dashboard" element={<DashboardPage />} isAuthenticated={user.isAuthenticated} />
</Routes>
```

### 11. Bagaimana cara menggunakan `<Link>` di React Router v6?

`<Link>` adalah komponen yang digunakan dalam React Router v6 untuk membuat tautan antar halaman dalam aplikasi React.

```js
import { Link } from 'react-router-dom';

const Navigation = () => {
  return (
    <nav>
      <ul>
        <li>
          {/* Membuat tautan ke halaman "/home" */}
          <Link to="/home">Home</Link>
        </li>
        <li>
          {/* Membuat tautan ke halaman "/about" */}
          <Link to="/about">About</Link>
        </li>
        <li>
          {/* Membuat tautan ke halaman "/contact" */}
          <Link to="/contact">Contact</Link>
        </li>
      </ul>
    </nav>
  );
};

export default Navigation;
```

Dalam contoh di atas, kita menggunakan `<Link>` untuk membuat tautan ke halaman-halaman dalam aplikasi kita. Properti to digunakan untuk menentukan rute yang ingin dituju oleh tautan tersebut. Ketika pengguna mengklik tautan, React Router
akan menavigasikan pengguna ke rute yang sesuai tanpa me-refresh seluruh halaman.

### 12. Apa perbedaan element prop di `<Route>` React Router v6 dibandingkan dengan component prop di versi sebelumnya?

- Pada React Router v5, kita mendefinisikan sebuah rute menggunakan komponen `<Route>`, kita memberikan properti component untuk menentukan komponen mana yang akan ditampilkan ketika rute tersebut diakses.

```js
import { Route } from 'react-router-dom';

<Route path="/home" component={Home} />;
```

- Pada React Router v6, kita menggunakan properti element untuk memberikan elemen React langsung yang akan ditampilkan.

```js
import { Route } from 'react-router-dom';

<Route path="/home" element={<Home />} />;
```

### 13. Bagaimana cara menerapkan lazy loading untuk komponen di React Router v6?

### 14. Apa kegunaan dari `useRoutes` hook dalam React Router v6?

useRoutes adalah hook yang digunakan dalam React Router v6 untuk menentukan rute-rute dalam aplikasi. Ini memungkinkan kita untuk menentukan rute-rute aplikasi secara dinamis berdasarkan logika yang kita tentukan.

```js
import { useRoutes } from 'react-router-dom';

const App = () => {
  const routeConfig = [
    { path: '/home', element: <HomePage /> },
    { path: '/about', element: <AboutPage /> },
    { path: '/contact', element: <ContactPage /> },
    { path: '*', element: <NotFoundPage /> },
  ];

  const routing = useRoutes(routeConfig);

  return routing;
};
```

### 15. Bagaimana cara menerapkan breadcrumbs dengan React Router v6?

### 16. Bagaimana cara menangani 404 page not found di React Router v6?

Menangani halaman 404 (Page Not Found) di React Router v6 cukup mudah. Kita dapat menggunakan rute wildcard (\*) untuk menangkap semua URL yang tidak cocok dengan rute-rute yang telah ditentukan sebelumnya. Di dalam rute wildcard ini, kita
dapat merender halaman 404.

1. Tentukan rute-rute aplikasi di dalam komponen Routes. Pastikan rute untuk halaman 404 diletakkan di akhir.

```js
import { Routes, Route } from 'react-router-dom';
import Home from './Home';
import About from './About';
import Contact from './Contact';
import NotFound from './NotFound'; // Halaman 404

const AppRoutes = () => {
  return (
    <Routes>
      <Route path="/" element={<Home />} />
      <Route path="/about" element={<About />} />
      <Route path="/contact" element={<Contact />} />
      {/* Rute wildcard untuk menangani halaman 404 */}
      <Route path="*" element={<NotFound />} />
    </Routes>
  );
};
```

2. Buat komponen untuk halaman 404, misalnya NotFound, di mana kita akan menampilkan pesan bahwa halaman tidak ditemukan.

```js
const NotFound = () => {
  return (
    <div>
      <h2>404 - Page Not Found</h2>
      <p>Sorry, the page you are looking for does not exist.</p>
    </div>
  );
};

export default NotFound;
```

### 17. Apa itu navigate function yang dikembalikan oleh useNavigate hook dan bagaimana menggunakannya?

Navigate function yang dikembalikan oleh useNavigate hook adalah sebuah fungsi yang digunakan untuk melakukan navigasi programatik (navigasi yang diinisiasi oleh kode) dalam React Router v6. Dengan menggunakan navigate function, kita dapat
melakukan navigasi antar halaman tanpa perlu menggunakan komponen Link atau Redirect.

```js
import { useNavigate } from 'react-router-dom';

const MyComponent = () => {
  const navigate = useNavigate();

  const handleClick = () => {
    // Melakukan navigasi ke halaman lain saat tombol diklik
    navigate('/about');
  };

  return (
    <div>
      <h1>Home Page</h1>
      <button onClick={handleClick}>Go to About Page</button>
    </div>
  );
};

export default MyComponent;
```

Dalam contoh di atas, kita menggunakan useNavigate hook untuk mendapatkan fungsi navigate. Ketika tombol diklik, fungsi handleClick akan dipanggil, dan di dalamnya kita menggunakan navigate function untuk melakukan navigasi ke halaman
'/about'.

### 18. Bagaimana cara menangani parameter opsional dalam rute di React Router v6?

Menangani parameter opsional dalam rute di React Router v6 bisa dilakukan dengan menambahkan tanda kurung kurawal ({}) di sekitar parameter yang bersifat opsional di dalam definisi rute. Ini memungkinkan kita untuk membuat parameter
tersebut opsional, artinya parameter tersebut dapat ada atau tidak dalam URL.

```js
import { Routes, Route } from 'react-router-dom';
import Home from './Home';
import ProductDetail from './ProductDetail'; // Komponen untuk halaman detail produk

const AppRoutes = () => {
  return (
    <Routes>
      <Route path="/" element={<Home />} />
      {/* Rute untuk halaman detail produk dengan parameter opsional */}
      <Route path="/products/:id?" element={<ProductDetail />} />
    </Routes>
  );
};
```

Dalam contoh di atas, kita menggunakan tanda tanya (?) setelah nama parameter (:id) untuk membuatnya opsional. Ini berarti bahwa parameter id dalam URL /products/:id adalah opsional. Dengan demikian, rute akan cocok dengan URL /products
tanpa parameter id, dan juga dengan URL /products/123 dengan parameter id.

### 19. Bagaimana cara menangani redirect berdasarkan kondisi di React Router v6?

Untuk menangani redirect berdasarkan kondisi di React Router v6, kita dapat menggunakan komponen `<Navigate>` bersama dengan logika kondisional untuk menentukan apakah akan melakukan redirect atau tidak.

```js
import { Navigate } from 'react-router-dom';

const MyComponent = ({ isLoggedIn }) => {
  // Jika pengguna tidak login, redirect ke halaman login
  if (!isLoggedIn) {
    return <Navigate to="/login" />;
  }

  // Jika pengguna login, tampilkan konten utama
  return (
    <div>
      <h1>Welcome to the main page!</h1>
      {/* Konten utama */}
    </div>
  );
};
```

Dalam contoh di atas, jika isLoggedIn bernilai false, maka `<Navigate>` akan meredirect pengguna ke halaman login. Jika isLoggedIn bernilai true, maka konten utama akan ditampilkan

### 20. Bagaimana cara mendefinisikan rute dengan beberapa parameter di React Router v6?

Untuk mendefinisikan rute dengan beberapa parameter di React Router v6, kita dapat menambahkan lebih dari satu parameter dalam path rute dan menggunakan sintaks :namaParameter untuk setiap parameter yang ingin kita tangkap dari URL.

```js
import { Routes, Route } from 'react-router-dom';
import ProductDetail from './ProductDetail'; // Komponen untuk halaman detail produk

const AppRoutes = () => {
  return (
    <Routes>
      {/* Rute untuk halaman detail produk dengan beberapa parameter */}
      <Route path="/products/:category/:id" element={<ProductDetail />} />
    </Routes>
  );
};
```

berdasarkan gambar diatas di dalam path rute, kita tambahkan dua parameter, yaitu :category dan :id, yang diawali dengan tanda titik dua (:). Ini akan membuat React Router menangkap nilai dari kedua parameter ini dari URL.

```js
import { useParams } from 'react-router-dom';

const ProductDetail = () => {
  const { category, id } = useParams();

  return (
    <div>
      <h2>Product Detail Page</h2>
      <p>Category: {category}</p>
      <p>Product ID: {id}</p>
      {/* Menampilkan detail produk berdasarkan category dan id */}
    </div>
  );
};

export default ProductDetail;
```

Ketika pengguna mengunjungi URL seperti /products/electronics/123, nilai category akan menjadi 'electronics' dan nilai id akan menjadi '123'.

### 21. Bagaimana cara menggunakan createBrowserRouter di React Router v6?

1. gunakan komponen <BrowserRouter> langsung dari package react-router-dom.
2. Bungkus komponen utama aplikasi dengan <BrowserRouter> di dalam file yang paling tinggi di hirarki aplikasi, biasanya di index.js

```js
import { BrowserRouter } from 'react-router-dom';

import React from 'react';
import ReactDOM from 'react-dom';
import App from './App'; // Ganti dengan nama file komponen utama aplikasi

ReactDOM.render(
  <React.StrictMode>
    {/* Gunakan <BrowserRouter> di dalam ReactDOM.render */}
    <BrowserRouter>
      <App />
    </BrowserRouter>
  </React.StrictMode>,
  document.getElementById('root')
);
```

### 22. Apa itu `<RouterProvider>` di React Router v6 dan bagaimana penggunaannya?

`<RouterProvider>` adalah komponen yang menyediakan router context kepada komponen-komponen di dalamnya. Ini memungkinkan komponen-komponen tersebut untuk mengakses berbagai fungsi dan data yang terkait dengan routing, seperti navigate,
location, dan params.

### 23. Bagaimana cara menggunakan createRoutesFromElements dalam React Router v6?

Dalam React Router v6, createRoutesFromElements digunakan untuk membuat rute-rute dari kumpulan elemen React. Ini memungkinkan kita untuk mendefinisikan rute-rute aplikasi kita secara dinamis dari kumpulan elemen yang sudah ada. Contoh:

```js
import { createRoutesFromElements, Route } from 'react-router-dom';

// Komponen-komponen yang akan menjadi rute-rute aplikasi
const Home = () => <h1>Home</h1>;
const About = () => <h1>About</h1>;
const Contact = () => <h1>Contact</h1>;

// Kumpulan elemen React yang akan diubah menjadi rute-rute
const routes = [<Route key="home" path="/" element={<Home />} />, <Route key="about" path="/about" element={<About />} />, <Route key="contact" path="/contact" element={<Contact />} />];

// Membuat rute-rute dari kumpulan elemen
const generatedRoutes = createRoutesFromElements(routes);

// Kemudian kita bisa menggunakan rute-rute ini dalam <Routes>
function App() {
  return <Routes>{generatedRoutes}</Routes>;
}
```

Dalam contoh ini, kita mendefinisikan komponen-komponen yang akan menjadi route aplikasi kita (Home, About, dan Contact). Kemudian, kita menempatkan komponen-komponen tersebut ke dalam elemen-elemen `<Route>` dengan properti path dan
element. Setelah itu, kita menggunakan createRoutesFromElements untuk mengonversi kumpulan elemen tersebut menjadi route yang siap digunakan dalam komponen `<Routes>`.

### 24. Apa itu resolvePath di React Router v6 dan bagaimana penggunaannya?

resolvePath digunakan untuk mendapatkan path lengkap dari suatu rute relatif terhadap path saat ini. Ini berguna ketika kita perlu membuat tautan atau mengarahkan pengguna ke suatu rute, terutama jika rute tersebut bersifat dinamis atau
bergantung pada konteks saat ini.

```js
import { useLocation, resolvePath } from 'react-router-dom';

function Navigation() {
  const location = useLocation();

  // Mendapatkan path lengkap dari rute '/about'
  const aboutPath = resolvePath('/about', location.pathname);

  return (
    <div>
      <p>Alamat lengkap rute About: {aboutPath}</p>
    </div>
  );
}
```

Dalam contoh ini, kita menggunakan resolvePath untuk mendapatkan alamat lengkap dari rute '/about' relatif terhadap path saat ini yang diperoleh dari `useLocation()`.

Di dalam variabel aboutPath, akan dikembalikan alamat lengkap dari rute '/about' relatif terhadap lokasi saat ini yang diperoleh dari useLocation(). Misalnya, jika lokasi saat ini adalah "/dashboard", dan alamat lengkap dari rute '/about'
adalah "/dashboard/about". Jadi, nilai yang akan dikembalikan di variabel aboutPath adalah "/dashboard/about".

### 25. Bagaimana cara mengimplementasikan search functionality menggunakan React Router v6?

kita membutuh sebuah komponen SearchBox. Komponen ini akan berisi input untuk mengetik kata kunci pencarian dan tombol untuk memulai pencarian.

```js
import { useState } from 'react';
import { useNavigate } from 'react-router-dom';

function SearchBox() {
  const [keyword, setKeyword] = useState('');
  const navigate = useNavigate();

  const handleSearch = () => {
    // Navigasi ke halaman pencarian dengan kata kunci yang dimasukkan
    navigate(`/search?keyword=${keyword}`);
  };

  return (
    <div>
      <input type="text" value={keyword} onChange={(e) => setKeyword(e.target.value)} placeholder="Search products..." />
      <button onClick={handleSearch}>Search</button>
    </div>
  );
}

export default SearchBox;
```

kemudian dapat menggunakan hook useParams untuk mengakses parameter pencarian dari URL dan menampilkannya sesuai kebutuhan.

````jsx
import { useParams } from 'react-router-dom';

function SearchResults() {
  const { keyword } = useParams();

  // Lakukan sesuatu dengan kata kunci pencarian, misalnya, ambil produk yang sesuai dari API

  return (
    <div>
      <h2>Search Results for "{keyword}"</h2>
      {/* Tampilkan hasil pencarian di sini */}
    </div>
  );
}

export default SearchResults;
```

### 26. Apa itu caseSensitive prop pada `<Route>` dan apa fungsinya?

### 27. Bagaimana cara mengekspos path sebagai prop ke komponen rute di React Router v6?

### 28. Apa itu basename dalam `<BrowserRouter>` dan bagaimana penggunaannya?

### 29. Bagaimana cara menggunakan createMemoryRouter di React Router v6?

### 30. Bagaimana cara menggunakan generatePath di React Router v6?
````
