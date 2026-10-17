{if(!active)return;active=false;if(e)e.preventDefault();if(up)up()};b.addEventListener('pointerup',end);b.addEventListener('pointercancel',end);b.addEventListener('lostpointercapture',end)};
tb('tj',()=>K.Space=true,()=>K.Space=false);
tb('ts',()=>K.ShiftLeft=true,()=>K.ShiftLeft=false);
tb('tn',()=>K.ControlLeft=true,()=>K.ControlLeft=false);
tb('tm1',()=>{if(locked){if(!atk())K.L=1}},()=>K.L=0);
tb('ta',()=>{if(locked&&!atk())K.L=1},()=>K.L=0);
tb('tp',()=>{if(locked)put()});
tb('ti',()=>{if(locked)put()});
tb('te',()=>{if(!dead)toggleCraft()});tb('tl',()=>pick(sel-1));tb('tr',()=>pick(sel+1));
tb('tf',()=>{if(!surv){fly=!fly;P.vy=0}else toast('Volar solo está disponible en Creativo')});
tb('tpa',()=>{saveW();locked=false;menu.style.display='flex'});
tb('tchat',()=>{const msg=prompt('Escribe un mensaje (chat local):');if(msg&&msg.trim())toast('Tú: '+msg.trim().slice(0,90))});
let emoteIndex=0;const emotes=['👋 ¡Hola!','👍 ¡Bien hecho!','😂 ¡Jajaja!','🎉 ¡Bien!'];
tb('temote',()=>{toast(emotes[emoteIndex%emotes.length]);emoteIndex++});
let last=performance.now();
function loop(t){
 requestAnimationFrame(loop);
 const dt=Math.min((t-last)/1000,.05);last=t;
 if(locked){update(dt);if(surv)live(dt);mobs(dt)}
 cam.position.set(P.x,P.y+1.62-((K.ControlLeft||K.KeyC)?.32:0),P.z);cam.rotation.set(P.pitch,P.yaw,0,'YXZ');
 const r=locked?ray():null;hl.visible=!!r;if(r)hl.position.set(r.x+.5,r.y+.5,r.z+.5);
 const mining=locked&&K.L&&r;
 if(mining){const kk=r.x+','+r.y+','+r.z;if(mk!=kk){mk=kk;mp=0}mp+=dt*mspd(get(r.x,r.y,r.z))/HD[get(r.x,r.y,r.z)];if(sw<=0)sw=1;if(mp>=1){brk(r);mp=0;mk=''}}else{mp=0;mk=''}
 crack.visible=mp>0&&!!r;if(r)crack.position.copy(hl.position);crack.material.opacity=mp*.7;
 sw=Math.max(0,sw-dt*4);const a=Math.sin(sw*Math.PI);handG.position.set(.36-a*.1,-.32-a*.1,-.55-a*.12);handG.rotation.set(.25-a*.9,.55,0);
 for(let i=PT.length-1;i>=0;i--){const m=PT[i];m.v.y-=15*dt;m.position.addScaledVector(m.v,dt);if((m.life-=dt)<0){scene.remove(m);m.material.dispose();PT.splice(i,1)}}
 tm=(tm+dt/300)%1;sky(dt);if(inGame)stream();flash=Math.max(0,flash-dt*2);dmgEl.style.opacity=flash*.45;
 renderer.render(scene,cam);
}
requestAnimationFrame(loop);
</script></body></html>
