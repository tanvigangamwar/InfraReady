# InfraReady
infrastructure and developmengt
import { useState } from 'react';
import { useNavigate } from 'react-router-dom';
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { Shield, ArrowRight, BarChart3, CheckCircle2, AlertTriangle, TrendingUp, Globe2, Zap, Lock } from 'lucide-react';
import { motion } from 'framer-motion';

export default function Welcome() {
  const [nickname, setNickname] = useState('');
  const navigate = useNavigate();

  const handleStart = () => {
    if (nickname.trim()) {
      navigate(`/quiz?nickname=${encodeURIComponent(nickname.trim())}`);
    }
  };

  return (
    <div className="min-h-screen bg-background flex flex-col overflow-hidden">
      {/* Nav */}
      <header className="px-6 py-5 flex items-center justify-between z-10">
        <div className="flex items-center gap-2.5">
          <div className="h-9 w-9 rounded-xl bg-primary flex items-center justify-center shadow-sm">
            <BarChart3 className="h-5 w-5 text-primary-foreground" />
          </div>
          <span className="font-bold text-xl tracking-tight text-foreground">InfraReady</span>
        </div>
        <div className="flex items-center gap-1.5 px-3 py-1.5 bg-muted rounded-full text-xs text-muted-foreground">
          <Lock className="h-3 w-3" />
          No login required
        </div>
      </header>

      {/* Hero */}
      <main className="flex-1 flex flex-col items-center justify-center px-6 py-8">
        <motion.div
          initial={{ opacity: 0, y: 24 }}
          animate={{ opacity: 1, y: 0 }}
          transition={{ duration: 0.55 }}
          className="max-w-xl w-full"
        >
          {/* Badge */}
          <div className="flex justify-center mb-6">
            <div className="inline-flex items-center gap-2 px-4 py-2 rounded-full bg-primary/10 border border-primary/20 text-primary text-xs font-semibold">
              <Zap className="h-3.5 w-3.5" />
              AI Readiness Gap Assessment Tool
            </div>
          </div>

          {/* Headline */}
          <h1 className="text-4xl sm:text-5xl font-extrabold tracking-tight text-foreground text-center leading-tight mb-5">
            Find out where AI gaps are
            <span className="block text-primary">blocking your project</span>
          </h1>

          <p className="text-muted-foreground text-center text-base sm:text-lg leading-relaxed mb-10 max-w-md mx-auto">
            A 10-question assessment for infrastructure teams. Get a <strong className="text-foreground">visual heatmap</strong>, <strong className="text-foreground">governance checklist</strong>, and <strong className="text-foreground">plain-language report</strong> — in under 5 minutes.
          </p>

          {/* Input Card */}
          <motion.div
            initial={{ opacity: 0, y: 12 }}
            animate={{ opacity: 1, y: 0 }}
            transition={{ delay: 0.2, duration: 0.4 }}
            className="bg-card rounded-2xl border border-border p-6 sm:p-8 shadow-md mb-6"
          >
            <p className="text-sm font-semibold text-foreground mb-1">Start your assessment</p>
            <p className="text-xs text-muted-foreground mb-4">Choose a nickname — no email, no account needed.</p>
            <div className="flex gap-3">
              <Input
                value={nickname}
                onChange={(e) => setNickname(e.target.value)}
                onKeyDown={(e) => e.key === 'Enter' && handleStart()}
                placeholder="e.g. ProjectLead_Nairobi"
                className="h-12 text-base"
                autoFocus
              />
              <Button
                onClick={handleStart}
                disabled={!nickname.trim()}
                className="h-12 px-6 gap-2 shrink-0 text-base font-semibold shadow-sm"
              >
                Begin
                <ArrowRight className="h-4 w-4" />
              </Button>
            </div>
          </motion.div>

          {/* Trust signals */}
          <div className="grid grid-cols-3 gap-3 mb-10">
            {[
              { icon: CheckCircle2, label: "4 Gap Categories", sub: "Data, Governance, Skills, Connectivity" },
              { icon: Globe2, label: "LMIC-Adapted", sub: "Works for Global South contexts" },
              { icon: Shield, label: "Privacy-First", sub: "No personal data collected" }
            ].map((item) => (
              <div key={item.label} className="flex flex-col items-center text-center p-3 rounded-xl bg-card border border-border">
                <item.icon className="h-5 w-5 text-primary mb-2" />
                <p className="text-xs font-semibold text-foreground leading-tight">{item.label}</p>
                <p className="text-[10px] text-muted-foreground mt-0.5 leading-tight">{item.sub}</p>
              </div>
            ))}
          </div>

          {/* Problem Statement */}
          <motion.div
            initial={{ opacity: 0 }}
            animate={{ opacity: 1 }}
            transition={{ delay: 0.4 }}
            className="bg-foreground rounded-2xl p-6 text-background"
          >
            <div className="flex items-start gap-3 mb-3">
              <AlertTriangle className="h-5 w-5 text-yellow-400 mt-0.5 shrink-0" />
              <p className="text-sm font-bold text-background leading-snug">
                Most infrastructure projects fail to adopt AI not because of technology — but because of invisible readiness gaps.
              </p>
            </div>
            <p className="text-xs text-background/70 leading-relaxed">
              Data quality issues, governance lag, skills gaps, and poor connectivity silently block decisions across energy, water, transport, and telecom projects. InfraReady makes these gaps visible in minutes.
            </p>
          </motion.div>
        </motion.div>
      </main>

      <footer className="px-6 py-4 text-center text-xs text-muted-foreground border-t border-border">
        InfraReady — Visual AI Gap Assessment for Infrastructure Teams
      </footer>
    </div>
  );
}

