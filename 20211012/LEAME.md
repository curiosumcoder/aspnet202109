0. Verificar la instalación del comando EF
	

1. Quitar la migración

	* dotnet ef migrations remove -c ApplicationDbContext			
	* dotnet ef migrations add IdentityNew -c ApplicationDbContext
	* dotnet ef database update -c ApplicationDbContext
	* dotnet ef migrations remove -c ApplicationDbContext
	* dotnet ef migrations add IdentityCustom -c ApplicationDbContext
	* dotnet ef database update -c ApplicationDbContext

2. Modificar el conexión y el Startup

3. Modificar el ApplicationDbContext

    public class ApplicationDbContext : IdentityDbContext
    {
        public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
            : base(options)
        {
        }

        protected override void OnModelCreating(ModelBuilder modelBuilder)
        {
            base.OnModelCreating(modelBuilder);

            modelBuilder.HasDefaultSchema("Auth");
        }
    }

4. Generar la migración y aplicarla

	dotnet ef migrations add IdentityNew -c ApplicationDbContext
	dotnet ef database update -c ApplicationDbContext

---------------------------------------------------------------------------------------
Area

                app.UseEndpoints(endpoints =>
                {
                    endpoints.MapControllerRoute(
                      name: "areas",
                      pattern: "{area:exists}/{controller=Home}/{action=Index}/{id?}"
                    );
                });


....
    [Area("Admin")]

---------------------------------------------------------------------------------------
	* dotnet tool install -g dotnet-aspnet-codegenerator
	* dotnet aspnet-codegenerator --help