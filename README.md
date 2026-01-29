import { useState, useEffect } from "react";
import { motion } from "framer-motion";
import { ShieldCheck, Calendar, ArrowRight, Truck, UserCheck, Info, Clock, DollarSign } from "lucide-react";
import { Button } from "@/components/ui/button";
import { Link } from "wouter";
import heroImage from "../assets/hero-truck-parking.png";
import { 
  Dialog, 
  DialogContent, 
  DialogHeader, 
  DialogTitle, 
  DialogDescription 
} from "@/components/ui/dialog";

export default function Hero() {
  const [language, setLanguage] = useState<"EN" | "ES">("EN");
  const [showRates, setShowRates] = useState(false);

  useEffect(() => {
    const handleLang = (e: any) => setLanguage(e.detail);
    window.addEventListener('language-change', handleLang);
    return () => window.removeEventListener('language-change', handleLang);
  }, []);

  return (
    <div className="relative min-h-[90vh] w-full overflow-hidden flex items-center justify-center bg-zinc-900">
      {/* Background Image with Overlay */}
      <div 
        className="absolute inset-0 z-0 bg-cover bg-center bg-no-repeat"
        style={{ 
          backgroundImage: `url(${heroImage})`,
        }}
      >
        <div className="absolute inset-0 bg-gradient-to-r from-zinc-900/90 via-zinc-900/70 to-zinc-900/30" />
      </div>

      <div className="container relative z-10 px-4 py-32 grid gap-8 md:grid-cols-2 items-center">
        <div className="space-y-8">
          <motion.div
            initial={{ opacity: 0, x: -20 }}
            animate={{ opacity: 1, x: 0 }}
            transition={{ duration: 0.5 }}
          >
            <div className="flex flex-col gap-4 mb-6">
              <div className="inline-flex items-center rounded-full border border-green-500/30 bg-green-500/10 px-3 py-1 text-sm font-bold text-green-400 backdrop-blur-md w-fit">
                <span className="flex h-2 w-2 rounded-full bg-green-400 mr-2 animate-pulse"></span>
                {language === "EN" ? "Lot Status: Open 24/7" : "Estado del Lote: Abierto 24/7"}
              </div>
              <div className="inline-flex items-center rounded-full border border-zinc-700 bg-zinc-800/50 px-3 py-1 text-sm text-zinc-100 backdrop-blur-md w-fit">
                <span className="flex h-2 w-2 rounded-full bg-accent mr-2 animate-pulse"></span>
                {language === "EN" ? " Nfl Truck & Trailer Parking" : "Estacionamiento de camiones y remolques de la NFL"}
              </div>
            </div>
            <h1 className="text-5xl font-bold tracking-tighter text-white sm:text-6xl xl:text-7xl mb-6" data-testid="text-hero-title">
              {language === "EN" ? "PREMIER TRUCK PARKING IN" : "ESTACIONAMIENTO PREMIER EN"}
              {" "}
              <span className="relative inline-block" data-testid="text-hero-city-wrap">
                <span className="relative z-10 text-accent" data-testid="text-hero-city">DALLAS</span>
              </span>
            </h1>
            <p className="max-w-[600px] text-zinc-300 text-lg md:text-xl leading-relaxed">
              {language === "EN" 
                ? "Secure, 24/7 accessible parking for semi-trucks, trailers, and logistics fleets. Lighted and monitored."
                : "Estacionamiento seguro y accesible 24/7 para camiones, remolques y flotas logísticas. Iluminado y monitoreado."}
            </p>
          </motion.div>

          <motion.div 
            initial={{ opacity: 0, y: 20 }}
            animate={{ opacity: 1, y: 0 }}
            transition={{ duration: 0.5, delay: 0.2 }}
            className="flex flex-col sm:flex-row gap-4 items-start"
          >
              <div className="flex flex-col items-center gap-4 w-full sm:w-auto">
                <Link href="/reserve" className="w-full sm:w-auto">
                  <motion.button
                    className="group relative overflow-hidden rounded-md bg-accent px-8 py-4 font-bold text-white shadow-lg transition-all hover:scale-105 hover:shadow-accent/25 active:scale-95 cursor-pointer w-full"
                    whileHover="hover"
                  >
                    <div className="relative z-10 flex items-center justify-center gap-2 uppercase tracking-wider">
                      <span>{language === "EN" ? "Reserve Now" : "Reservar Ahora"}</span>
                      <ArrowRight className="h-5 w-5" />
                    </div>
                    
                    <motion.div
                      variants={{
                        hover: { y: 0, opacity: 1 }
                      }}
                      initial={{ y: "100%", opacity: 0 }}
                      transition={{ type: "spring", stiffness: 300, damping: 20 }}
                      className="absolute inset-0 z-20 flex items-center justify-center gap-2 bg-primary font-bold uppercase tracking-wider text-white"
                    >
                      <ShieldCheck className="h-5 w-5" />
                      <span>{language === "EN" ? "Safe Parking" : "Lugar Seguro"}</span>
                    </motion.div>
                  </motion.button>
                </Link>
                <div className="flex flex-col items-center gap-1 w-full sm:w-auto">
                  <motion.button
                    onClick={() => {
                      window.dispatchEvent(new CustomEvent('open-check-in'));
                    }}
                    className="group relative overflow-hidden rounded-md border-2 border-accent bg-transparent px-8 py-3 font-bold text-accent shadow-lg transition-all hover:scale-105 hover:bg-accent hover:text-white active:scale-95 cursor-pointer w-full sm:w-auto"
                    whileHover="hover"
                  >
                    <div className="relative z-10 flex items-center justify-center gap-2 uppercase tracking-wider text-xs">
                      <UserCheck className="h-4 w-4" />
                      <span>{language === "EN" ? "Check-In" : "Registrarse"}</span>
                    </div>

                    <motion.div
                      variants={{
                        hover: { y: 0, opacity: 1 }
                      }}
                      initial={{ y: "100%", opacity: 0 }}
                      transition={{ type: "spring", stiffness: 300, damping: 20 }}
                      className="absolute inset-0 z-20 flex items-center justify-center gap-2 bg-accent font-bold uppercase tracking-wider text-white"
                    >
                      <Clock className="h-4 w-4" />
                      <span>{language === "EN" ? "Confirm Arrival" : "Confirmar Llegada"}</span>
                    </motion.div>
                  </motion.button>
                  <span className="text-[9px] font-black text-accent/50 uppercase tracking-[0.2em]">
                    {language === "EN" ? "Reserve First" : "Reservar Primero"}
                  </span>
                </div>
              </div>
            
            <div className="w-full sm:w-auto">
              <motion.button
                onClick={() => setShowRates(true)}
                className="group relative overflow-hidden rounded-md border-2 border-accent bg-transparent px-8 py-4 font-bold text-accent shadow-lg transition-all hover:scale-105 hover:bg-accent hover:text-white active:scale-95 cursor-pointer w-full"
                whileHover="hover"
              >
                <div className="relative z-10 flex items-center justify-center gap-2 uppercase tracking-wider">
                  <span>{language === "EN" ? "View Rates" : "Ver Tarifas"}</span>
                </div>

                <motion.div
                  variants={{
                    hover: { y: 0, opacity: 1 }
                  }}
                  initial={{ y: "100%", opacity: 0 }}
                  transition={{ type: "spring", stiffness: 300, damping: 20 }}
                  className="absolute inset-0 z-20 flex items-center justify-center gap-2 bg-accent font-bold uppercase tracking-wider text-white"
                >
                  <DollarSign className="h-5 w-5" />
                  <span>{language === "EN" ? "Price List" : "Lista de Precios"}</span>
                </motion.div>
              </motion.button>
            </div>
          </motion.div>
        </div>

        {/* Floating Card Element */}
        <motion.div
          initial={{ opacity: 0, scale: 0.9 }}
          animate={{ opacity: 1, scale: 1 }}
          transition={{ duration: 0.7, delay: 0.4 }}
          className="hidden md:block"
        >
          <div className="relative rounded-xl border border-white/10 bg-zinc-900/50 p-8 backdrop-blur-md shadow-2xl">
            <div className="grid gap-6">
              <div className="flex items-center gap-4">
                <div className="flex h-12 w-12 items-center justify-center rounded-lg bg-primary text-primary-foreground">
                  <ShieldCheck className="h-6 w-6" />
                </div>
                <div>
                  <h3 className="font-bold text-white text-lg">{language === "EN" ? "24/7 Security" : "Seguridad 24/7"}</h3>
                  <p className="text-zinc-400">{language === "EN" ? "Gated access with CCTV monitoring" : "Acceso cerrado con monitoreo CCTV"}</p>
                </div>
              </div>
              
              <div className="h-px bg-white/10" />
              
              <div className="flex items-center gap-4">
                <div className="flex h-12 w-12 items-center justify-center rounded-lg bg-primary text-primary-foreground">
                  <Calendar className="h-6 w-6" />
                </div>
                <div>
                  <h3 className="font-bold text-white text-lg">{language === "EN" ? "Flexible Terms" : "Términos Flexibles"}</h3>
                  <p className="text-zinc-400">{language === "EN" ? "Daily, weekly, and monthly rates" : "Tarifas diarias, semanales y mensuales"}</p>
                </div>
              </div>
            </div>
          </div>
        </motion.div>
      </div>

      <Dialog open={showRates} onOpenChange={setShowRates}>
        <DialogContent className="sm:max-w-md border-t-4 border-t-accent bg-zinc-900 text-white">
          <DialogHeader>
            <DialogTitle className="text-2xl font-black uppercase tracking-tighter text-accent flex items-center gap-2">
              <Info className="h-6 w-6" />
              {language === "EN" ? "Current Rates" : "Tarifas Actuales"}
            </DialogTitle>
            <DialogDescription className="font-bold text-zinc-400 uppercase tracking-tight text-xs">
              {language === "EN" ? "Professional Parking Solutions in Dallas" : "Soluciones de Estacionamiento Profesional en Dallas"}
            </DialogDescription>
          </DialogHeader>
          <div className="space-y-6 py-6">
            <div className="grid grid-cols-1 gap-4">
              <div className="p-6 rounded-xl bg-zinc-800 border-2 border-zinc-700 flex justify-between items-center group hover:border-accent transition-colors">
                <div>
                  <h4 className="text-lg font-black uppercase tracking-widest text-white">
                    {language === "EN" ? "Truck Only" : "Solo Camión"}
                  </h4>
                  <p className="text-sm text-zinc-400 font-bold uppercase tracking-tight">
                    {language === "EN" ? "Semi-Tractor Unit" : "Unidad de Tractocamión"}
                  </p>
                </div>
                <div className="text-right">
                  <span className="text-3xl font-black text-accent">$150</span>
                  <span className="block text-[10px] font-black text-zinc-500 uppercase">/ {language === "EN" ? "Month" : "Mes"}</span>
                </div>
              </div>

              <div className="p-6 rounded-xl bg-zinc-800 border-2 border-zinc-700 flex justify-between items-center group hover:border-accent transition-colors">
                <div>
                  <h4 className="text-lg font-black uppercase tracking-widest text-white">
                    {language === "EN" ? "Truck + Trailer" : "Camión + Remolque"}
                  </h4>
                  <p className="text-sm text-zinc-400 font-bold uppercase tracking-tight">
                    {language === "EN" ? "Full 53' Combination" : "Combinación Completa de 53'"}
                  </p>
                </div>
                <div className="text-right">
                  <span className="text-3xl font-black text-accent">$200</span>
                  <span className="block text-[10px] font-black text-zinc-500 uppercase">/ {language === "EN" ? "Month" : "Mes"}</span>
                </div>
              </div>
            </div>
            
            <div className="p-4 rounded-lg bg-accent/10 border border-accent/20">
              <p className="text-[10px] font-black text-accent uppercase tracking-widest text-center leading-relaxed">
                {language === "EN" 
                  ? "* Daily rates ($15/day) available for smaller units in the booking form" 
                  : "* Tarifas diarias ($15/día) disponibles para unidades más pequeñas en el formulario"}
              </p>
            </div>
            
            <Link href="/reserve" onClick={() => setShowRates(false)}>
              <Button className="w-full h-14 bg-accent hover:bg-accent/90 text-white font-black uppercase tracking-widest text-lg shadow-lg">
                {language === "EN" ? "Book Now" : "Reservar Ahora"}
              </Button>
            </Link>
          </div>
        </DialogContent>
      </Dialog>
    </div>
  );
}
