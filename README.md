const express = require('express');
const mongoose = require('mongoose');
const productRoutes = require('./routes/products');
const app = express();

// Conexión a MongoDB
mongoose.connect('mongodb://localhost:27017/BIGDATAPROJECT', {
  useNewUrlParser: true,
  useUnifiedTopology: true
});

// Configuración de EJS como motor de plantillas
app.set('view engine', 'ejs');

// Rutas (ejemplo básico)
app.get('/', (req, res) => {
  res.render('index');
});

const PORT = 3000;
app.listen(PORT, () => {
  console.log(`Server is running on http://localhost:${PORT}`);
});

app.use('/products', productRoutes);

// app.js

const http = require('http').Server(app);
const io = require('socket.io')(http);

io.on('connection', (socket) => {
    console.log('Usuario conectado');

    socket.on('disconnect', () => {
        console.log('Usuario desconectado');
    });

    // Aquí puedes añadir más eventos según lo que quieras monitorizar.
});

http.listen(PORT, () => {
    console.log(`Server is running on http://localhost:${PORT}`);
});
