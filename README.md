# Module 3: Creating and Consuming ASP.NET Core Web APIs 

# Lab: Creating an ASP.NET Core Web API

1. **Nombres y apellidos:** Francisco Javier Moreno Quevedo
2. **Fecha:** 17/01/2021
3. **Resumen del Ejercicio:**  Crear una ASP.NET Core Web API basica con un controlador
4. **Dificultad o problemas presentados y como se resolvieron:** Ninguna



#### Exercise 1: Create a controller class

- Abrimos en VSC el proyecto Starter del laboratorio

- Creamos el controlador **HotelBookingController** y añadimos

  ```cs
  using System.Threading.Tasks;
  using DAL.Models;
  using DAL.Repository;
  using Microsoft.AspNetCore.Mvc;
  
  namespace BlueYonder.Hotels.Service.Controllers
  {
  
       [Route("api/[controller]")]
       [ApiController]
       public class HotelBookingController : ControllerBase
       {
          private HotelBookingRepository repo;
  
          public HotelBookingController()
          {
              repo = new HotelBookingRepository();
          } 
  
           // GET api/HotelBooking/5
          [HttpGet("{id}")]
          public async Task<ActionResult<Booking>> Get(int id)
          {
              Booking booking = await repo.GetBooking(id);
              if (booking != null)
                  return Ok(booking);
              else
                  return NotFound();
          }
       
           // POST api/HotelBooking
           [HttpPost]
           public async Task<ActionResult> Post([FromBody] Booking booking)
           {
               if (!ModelState.IsValid) return BadRequest(ModelState);
               Booking BookingDb = await repo.Add(booking);
               if (BookingDb != null)
                   return Ok(BookingDb);
               else
                   return StatusCode(500);
           }
  
          // PUT api/HotelBooking/1
           [HttpPut("{id}")]
           public async Task<ActionResult<Booking>> Put(int id, [FromBody] Booking booking)
           {
               if (!ModelState.IsValid) return BadRequest(ModelState);
  
               Booking updatedBooking = await repo.Update(booking);
               return Ok(updatedBooking);
           }
  	}
  }
  ```

  

#### Exercise 2: Use the API from a browser

- Ejecutamos

- Comprobamos en el navegador que nos devuelve valores

```url
http://localhost:5000/api/HotelBooking/1
```

>