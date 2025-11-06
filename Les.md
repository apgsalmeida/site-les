**import React, { useState, useMemo } from "react";**



**// Plataforma educativa sobre Lúpus Eritematoso Sistêmico**

**// Arquivo único React + Tailwind (preview-ready). Default export é o componente principal.**



**export default function LupusEduPlatform() {**

  **const \[query, setQuery] = useState("");**

  **const \[activeSection, setActiveSection] = useState("home");**

  **const \[showAllResources, setShowAllResources] = useState(false);**



  **const sections = useMemo(() => ({**

    **home: {**

      **title: "Início",**

      **content: `Bem-vindo(a) à Plataforma Educativa sobre Lúpus Eritematoso Sistêmico (LES). Aqui você encontrará**

      **informações confiáveis, linguagem acessível e recursos práticos para pacientes, familiares e profissionais de saúde.`**

    **},**

    **about: {**

      **title: "O que é Lúpus",**

      **content: `Lúpus Eritematoso Sistêmico (LES) é uma doença autoimune que pode afetar pele, articulações, rins, pulmões, sistema nervoso e outros órgãos.**

      **A apresentação clínica varia muito entre pessoas — por isso é conhecida como doença "multissistêmica".`**

    **},**

    **symptoms: {**

      **title: "Sintomas",**

      **bullets: \[**

        **"Fadiga intensa e inexplicada",**

        **"Dor e inchaço nas articulações",**

        **"Erupções cutâneas (ex.: lesão em asa de borboleta no rosto)",**

        **"Febre de origem indeterminada",**

        **"Sensibilidade ao sol (fotossensibilidade)",**

        **"Problemas renais (proteinúria, alterações laboratoriais)",**

        **"Sintomas neurológicos (cefaleia, confusão, convulsões em casos raros)"**

      **]**

    **},**

    **diagnosis: {**

      **title: "Diagnóstico",**

      **content: `O diagnóstico de LES combina avaliação clínica com exames laboratoriais. Alguns testes importantes incluem: hemograma,**

      **prova de função renal, urina, autoanticorpos (ANA, anti-dsDNA, anti-Sm) e exames de imagem conforme a manifestação.`**

    **},**

    **treatment: {**

      **title: "Tratamento",**

      **bullets: \[**

        **"Educação e autocuidado",**

        **"Anti-inflamatórios e analgésicos para sintomas articulares",**

        **"Corticosteroides para crises inflamatórias agudas",**

        **"Antimaláricos (ex.: hidroxicloroquina) para controle de doença de pele e articulações",**

        **"Imunossupressores em casos graves (ex.: azatioprina, micofenolato)",**

        **"Novas terapias biológicas direcionadas a mecanismos específicos"**

      **]**

    **},**

    **living: {**

      **title: "Viver com Lúpus",**

      **content: `Viver com LES envolve monitoramento regular, plano de tratamento individualizado e medidas de suporte:**

      **proteção solar, vacinação conforme orientação médica, gerenciamento do estresse, atividade física adaptada, e suporte psicossocial.`**

    **},**

    **faqs: {**

      **title: "Perguntas Frequentes",**

      **faqs: \[**

        **{ q: "Lúpus tem cura?", a: "Atualmente não existe cura, mas a maioria das pessoas alcança controle dos sintomas com tratamento adequado." },**

        **{ q: "Lúpus é hereditário?", a: "Existe predisposição genética, mas fatores ambientais e hormonais também influenciam o risco." },**

        **{ q: "Posso engravidar com lúpus?", a: "Sim — porém é essencial planejamento com equipe especializada (reumatologista + obstetra de alto risco)." }**

      **]**

    **},**

    **resources: {**

      **title: "Recursos e Leituras",**

      **list: \[**

        **{ title: "Guia para Pacientes: Lúpus", type: "PDF/guia", url: "#" },**

        **{ title: "Associação de Pacientes - Apoio Local", type: "Organização", url: "#" },**

        **{ title: "Diretrizes Clínicas para LES", type: "Artigo", url: "#" }**

      **]**

    **}**

  **}), \[]);**



  **const allContent = useMemo(() => {**

    **// Combina texto para busca simples**

    **const flat = \[];**

    **Object.keys(sections).forEach((k) => {**

      **const s = sections\[k];**

      **flat.push((s.title || "") + " " + (s.content || "") );**

      **if (s.bullets) flat.push(s.bullets.join(" "));**

      **if (s.faqs) flat.push(s.faqs.map(f => f.q + ' ' + f.a).join(' '));**

      **if (s.list) flat.push(s.list.map(r => r.title).join(' '));**

    **});**

    **return flat.join(" \\n");**

  **}, \[sections]);**



  **const results = useMemo(() => {**

    **if (!query.trim()) return null;**

    **const q = query.toLowerCase();**

    **const hits = \[];**

    **Object.keys(sections).forEach((k) => {**

      **const s = sections\[k];**

      **const hay = (s.title + ' ' + (s.content || '') + ' ' + (s.bullets ? s.bullets.join(' ') : '')).toLowerCase();**

      **if (hay.includes(q)) hits.push({ key: k, title: s.title });**

    **});**

    **return hits;**

  **}, \[query, sections]);**



  **const handlePrint = () => {**

    **window.print();**

  **};**



  **return (**

    **<div className="min-h-screen bg-gray-50 text-gray-900">**

      **<header className="bg-white shadow">**

        **<div className="max-w-6xl mx-auto px-4 py-4 flex items-center justify-between">**

          **<div className="flex items-center gap-3">**

            **<div className="w-11 h-11 rounded-full bg-gradient-to-br from-indigo-500 to-pink-500 flex items-center justify-center text-white font-bold">LE</div>**

            **<div>**

              **<h1 className="text-xl font-semibold">Plataforma Educativa - Lúpus Eritematoso Sistêmico</h1>**

              **<p className="text-sm text-gray-600">Informações confiáveis para pacientes, familiares e profissionais.</p>**

            **</div>**

          **</div>**



          **<nav className="hidden md:flex gap-2 items-center">**

            **{Object.keys(sections).map((k) => (**

              **<button**

                **key={k}**

                **onClick={() => setActiveSection(k)}**

                **className={`px-3 py-2 rounded-md text-sm font-medium ${activeSection === k ? 'bg-indigo-600 text-white' : 'text-gray-700 hover:bg-gray-100'}`}>**

                **{sections\[k].title}**

              **</button>**

            **))}**

            **<button onClick={handlePrint} className="ml-3 px-3 py-2 bg-gray-100 rounded-md text-sm">Imprimir</button>**

          **</nav>**



          **<div className="ml-4 md:ml-0">**

            **<label htmlFor="search" className="sr-only">Pesquisar</label>**

            **<input**

              **id="search"**

              **type="search"**

              **value={query}**

              **onChange={(e) => setQuery(e.target.value)}**

              **placeholder="Pesquisar conteúdo..."**

              **className="w-56 md:w-72 px-3 py-2 border rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-300"**

              **aria-label="Pesquisar conteúdo da plataforma"**

            **/>**

          **</div>**

        **</div>**

      **</header>**



      **<main className="max-w-6xl mx-auto px-4 py-8 grid grid-cols-1 md:grid-cols-3 gap-6">**

        **<aside className="md:col-span-1 bg-white p-4 rounded-lg shadow-sm">**

          **<h2 className="text-lg font-semibold">Navegação</h2>**

          **<ul className="mt-3 space-y-2">**

            **{Object.keys(sections).map((k) => (**

              **<li key={k}>**

                **<button onClick={() => { setActiveSection(k); window.scrollTo({ top: 0, behavior: 'smooth' }); }}**

                  **className={`w-full text-left px-3 py-2 rounded-md ${activeSection === k ? 'bg-indigo-50' : 'hover:bg-gray-50'}`}>**

                  **{sections\[k].title}**

                **</button>**

              **</li>**

            **))}**

          **</ul>**



          **<div className="mt-6">**

            **<h3 className="text-sm font-medium">Recursos rápidos</h3>**

            **<ul className="mt-2 space-y-2 text-sm">**

              **{sections.resources.list.slice(0, showAllResources ? sections.resources.list.length : 2).map((r, i) => (**

                **<li key={i} className="flex justify-between items-center">**

                  **<span>{r.title}</span>**

                  **<a href={r.url} className="text-indigo-600 text-sm">Abrir</a>**

                **</li>**

              **))}**

            **</ul>**

            **<button onClick={() => setShowAllResources(s => !s)} className="mt-3 text-sm text-indigo-600">{showAllResources ? 'Mostrar menos' : 'Ver todos'}</button>**

          **</div>**



          **<div className="mt-6 text-sm text-gray-600">**

            **<p><strong>Aviso:</strong> Este site fornece informação educativa e não substitui avaliação médica. Consulte um profissional de saúde para diagnóstico e tratamento.</p>**

          **</div>**

        **</aside>**



        **<section className="md:col-span-2 space-y-6">**

          **{/\* Search results \*/}**

          **{results \&\& (**

            **<div className="bg-yellow-50 border-l-4 border-yellow-400 p-4 rounded-md">**

              **<strong>Resultados para:</strong> "{query}" — {results.length} seção(ões) encontrada(s).**

              **<div className="mt-2 flex gap-2 flex-wrap">**

                **{results.map(r => (**

                  **<button key={r.key} onClick={() => setActiveSection(r.key)} className="px-3 py-1 bg-white rounded shadow-sm text-sm">Ir para: {r.title}</button>**

                **))}**

              **</div>**

            **</div>**

          **)}**



          **{/\* Content render \*/}**

          **<article className="bg-white p-6 rounded-lg shadow-sm">**

            **<h2 className="text-2xl font-bold">{sections\[activeSection].title}</h2>**



            **{/\* Home and text sections \*/}**

            **{sections\[activeSection].content \&\& (**

              **<p className="mt-4 text-gray-700 leading-relaxed">{sections\[activeSection].content}</p>**

            **)}**



            **{/\* Bulleted lists \*/}**

            **{sections\[activeSection].bullets \&\& (**

              **<ul className="mt-4 list-disc list-inside space-y-2 text-gray-700">**

                **{sections\[activeSection].bullets.map((b, i) => <li key={i}>{b}</li>)}**

              **</ul>**

            **)}**



            **{/\* FAQs \*/}**

            **{sections\[activeSection].faqs \&\& (**

              **<div className="mt-6">**

                **<h3 className="font-semibold">Perguntas Frequentes</h3>**

                **<div className="mt-3 space-y-3">**

                  **{sections\[activeSection].faqs.map((f, i) => (**

                    **<details key={i} className="p-3 bg-gray-50 rounded">**

                      **<summary className="font-medium cursor-pointer">{f.q}</summary>**

                      **<p className="mt-2 text-gray-700">{f.a}</p>**

                    **</details>**

                  **))}**

                **</div>**

              **</div>**

            **)}**



            **{/\* Resources list \*/}**

            **{activeSection === 'resources' \&\& (**

              **<div className="mt-6">**

                **<h3 className="font-semibold">Recursos</h3>**

                **<ul className="mt-3 space-y-2">**

                  **{sections.resources.list.map((r, i) => (**

                    **<li key={i} className="p-3 border rounded flex justify-between items-center">**

                      **<div>**

                        **<div className="font-medium">{r.title}</div>**

                        **<div className="text-sm text-gray-500">{r.type}</div>**

                      **</div>**

                      **<a href={r.url} className="text-indigo-600">Abrir</a>**

                    **</li>**

                  **))}**

                **</ul>**

              **</div>**

            **)}**



            **{/\* Contact form on reach \*/}**

            **{activeSection === 'home' \&\& (**

              **<div className="mt-6 p-4 bg-indigo-50 rounded">**

                **<h3 className="font-semibold">Fale conosco</h3>**

                **<form onSubmit={(e) => { e.preventDefault(); alert('Mensagem enviada (simulação).'); }} className="mt-3 space-y-3">**

                  **<div>**

                    **<label className="text-sm">Nome</label>**

                    **<input required className="w-full px-3 py-2 border rounded" placeholder="Seu nome" />**

                  **</div>**

                  **<div>**

                    **<label className="text-sm">Email</label>**

                    **<input type="email" required className="w-full px-3 py-2 border rounded" placeholder="seu@exemplo.com" />**

                  **</div>**

                  **<div>**

                    **<label className="text-sm">Mensagem</label>**

                    **<textarea required className="w-full px-3 py-2 border rounded" rows={4} placeholder="Escreva sua mensagem..."></textarea>**

                  **</div>**

                  **<div className="flex gap-2">**

                    **<button type="submit" className="px-4 py-2 bg-indigo-600 text-white rounded">Enviar</button>**

                    **<button type="button" onClick={() => { setQuery(''); alert('Exemplo: formulário não envia na demo.'); }} className="px-4 py-2 border rounded">Limpar</button>**

                  **</div>**

                **</form>**

              **</div>**

            **)}**



          **</article>**



          **{/\* Additional educational card \*/}**

          **<div className="bg-white p-4 rounded-lg shadow-sm">**

            **<h3 className="font-semibold">Ferramentas práticas</h3>**

            **<div className="mt-3 grid grid-cols-1 sm:grid-cols-2 gap-3">**

              **<button onClick={() => { navigator.clipboard?.writeText(window.location.href); alert('Link copiado para a área de transferência.'); }} className="px-3 py-2 border rounded text-sm">Copiar link da página</button>**

              **<button onClick={handlePrint} className="px-3 py-2 border rounded text-sm">Gerar PDF (imprimir)</button>**

            **</div>**

          **</div>**



          **{/\* Small footer \*/}**

          **<div className="text-xs text-gray-500 mt-2">Conteúdo educativo — não substitui orientação médica.</div>**



        **</section>**

      **</main>**



      **<footer className="bg-white border-t">**

        **<div className="max-w-6xl mx-auto px-4 py-6 flex flex-col md:flex-row justify-between items-center gap-3">**

          **<div className="text-sm text-gray-600">© {new Date().getFullYear()} Plataforma Educativa - LES. Todos os direitos reservados.</div>**

          **<div className="flex gap-3">**

            **<a href="#" className="text-sm text-indigo-600">Política de privacidade</a>**

            **<a href="#" className="text-sm text-indigo-600">Termos</a>**

          **</div>**

        **</div>**

      **</footer>**

    **</div>**

  **);**

**}**



