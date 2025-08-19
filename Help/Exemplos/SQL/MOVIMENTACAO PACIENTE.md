select 
a.nr_atendimento,
c.nm_pessoa_fisica,
c.dt_nascimento,
c.ie_sexo,
b.dt_entrada_unidade, 
substr(tasy.obter_nome_setor(cd_setor_atendimento),1,100) ds_setor_atendimento, 
b.cd_unidade_basica, 
b.cd_unidade_compl, 
b.dt_saida_unidade, 
substr(tasy.obter_desc_tipo_acomod(b.cd_tipo_acomodacao),1,100) ds_tipo_acomodacao 
from tasy.atendimento_paciente a, 
tasy.atend_paciente_unidade b,
tasy.pessoa_fisica c
where a.nr_atendimento = b.nr_atendimento
and a.cd_pessoa_fisica = c.cd_pessoa_fisica
and to_char(b.dt_entrada_unidade,'dd/mm/yyyy') between :dt_inicio and :dt_fim
and cd_setor_atendimento in (6,89,53,52,51,74,76,88,54)
order by nm_pessoa_fisica