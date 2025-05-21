# Calendario-FEMEC-OC
import React, { useState } from "react"; import { Card, CardContent } from "/components/ui/card"; import { Button } from "/components/ui/button"; import { Input } from "/components/ui/input"; import { Calendar } from "/components/ui/calendar"; import { Bell, Search, CalendarDays, User, FileText, LogIn, Filter, PieChart } from "lucide-react"; import { motion } from "framer-motion";

const events = [ { date: "2025-05-25", title: "Aniversário Igreja Central", type: "Aniversário", location: "Igreja Central" }, { date: "2025-05-28", title: "Congresso de Jovens", type: "Evento", location: "Auditório Central" }, ];

const updates = [ { date: "2025-05-20", description: "Evento 'Aniversário Igreja Central' adicionado." }, { date: "2025-05-18", description: "Correção no nome da igreja da Zona Sul." }, ];

export default function CalendarApp() { const [selectedDate, setSelectedDate] = useState(new Date()); const [search, setSearch] = useState(""); const filteredEvents = events.filter(e => e.title.toLowerCase().includes(search.toLowerCase()));

return ( <motion.div className="grid grid-cols-4 gap-4 p-4 bg-black text-white min-h-screen" initial={{ opacity: 0 }} animate={{ opacity: 1 }}>

{/* Notificações e Histórico */}
  <div className="col-span-1 space-y-4">
    <Card className="bg-zinc-900 rounded-2xl shadow-xl">
      <CardContent className="p-4">
        <div className="flex items-center gap-2 mb-2"><Bell className="text-yellow-400" /> Notificações</div>
        <ul className="text-sm list-disc list-inside">
          <li>Lembrete: Reunião amanhã às 18h</li>
          <li>Atualização: Evento 'Congresso' movido para 28/05</li>
        </ul>
      </CardContent>
    </Card>

    <Card className="bg-zinc-900 rounded-2xl shadow-xl">
      <CardContent className="p-4">
        <div className="flex items-center gap-2 mb-2"><FileText className="text-blue-400" /> Histórico de alterações</div>
        <ul className="text-xs list-disc list-inside">
          {updates.map((u, i) => <li key={i}>{u.date}: {u.description}</li>)}
        </ul>
      </CardContent>
    </Card>

    <Card className="bg-zinc-900 rounded-2xl shadow-xl">
      <CardContent className="p-4">
        <div className="flex items-center gap-2 mb-2"><LogIn className="text-pink-400" /> Login & Autenticação</div>
        <p className="text-sm text-zinc-300">Acesso com autenticação via e-mail ou redes sociais.</p>
      </CardContent>
    </Card>
  </div>

  {/* Calendário e Busca */}
  <div className="col-span-3 space-y-4">
    <div className="flex justify-between items-center">
      <div className="text-xl font-semibold flex gap-2 items-center"><CalendarDays /> Calendário de Programações</div>
      <div className="flex gap-2 w-1/2">
        <Input placeholder="Buscar eventos..." className="w-full bg-zinc-800 border-zinc-700" value={search} onChange={(e) => setSearch(e.target.value)} />
        <Button variant="outline" className="text-white border-zinc-600"><Filter /> Filtros</Button>
      </div>
    </div>

    <div className="grid grid-cols-4 gap-4">
      {filteredEvents.map((event, i) => (
        <Card key={i} className="bg-zinc-800 text-white p-4 rounded-2xl border-l-4 border-green-400 shadow hover:scale-105 transition">
          <div className="text-sm text-zinc-400">{event.date}</div>
          <div className="font-bold text-lg">{event.title}</div>
          <div className="text-sm italic text-zinc-300">{event.type} - {event.location}</div>
          <div className="mt-2 flex gap-2 text-xs">
            <Button size="sm" className="bg-green-600 hover:bg-green-700">Confirmar Presença</Button>
            <Button size="sm" className="bg-blue-600 hover:bg-blue-700">Anexar Arquivo</Button>
          </div>
        </Card>
      ))}
    </div>

    <Card className="bg-zinc-900 rounded-2xl p-4">
      <div className="text-lg mb-2 flex items-center gap-2"><User className="text-purple-400" /> Perfis e Permissões</div>
      <p className="text-sm text-zinc-300">Usuários podem visualizar, editar ou aprovar eventos conforme sua permissão. Confirmações de presença (RSVP) estão disponíveis nos eventos com ícones de status.</p>
    </Card>

    <Card className="bg-zinc-900 rounded-2xl p-4">
      <div className="text-lg mb-2">Widget de Destaque</div>
      <p className="text-sm text-yellow-300 font-medium">Próximo evento: Congresso de Jovens em 28/05</p>
    </Card>

    <Card className="bg-zinc-900 rounded-2xl p-4">
      <div className="text-lg mb-2 flex items-center gap-2"><PieChart className="text-green-400" /> Relatórios de Atividades</div>
      <p className="text-sm text-zinc-300">Resumo mensal disponível com eventos confirmados, alterações realizadas e anexos adicionados.</p>
    </Card>

    <Calendar mode="single" selected={selectedDate} onSelect={setSelectedDate} className="rounded-md border border-zinc-700 bg-zinc-800 p-2 text-white" />
  </div>
</motion.div>

); }

