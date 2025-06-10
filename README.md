# Poai-kr
class Rule:
    def __init__(self, premise, conclusion):
        self.premise = premise
        self.conclusion = conclusion

class KnowledgeBase:
    def __init__(self):
        self.rules = []
        self.facts = set()

  def add_rule(self, rule):
        self.rules.append(rule)

   def add_fact(self, fact):
        self.facts.add(fact)

   def query(self, query):
        if query in self.facts:
            return True
        for rule in self.rules:
            if rule.conclusion == query and self.evaluate_premise(rule.premise):
                return True
        return False

  def evaluate_premise(self, premise):
        if premise in self.facts:
            return True
        for rule in self.rules:
            if rule.conclusion == premise and self.evaluate_premise(rule.premise):
                return True
        return False

class DecisionMaker:
    def __init__(self, knowledge_base):
        self.knowledge_base = knowledge_base

  def make_decision(self, query):
        if self.knowledge_base.query(query):
            return f"The decision is: {query}"
        else:
            return f"The decision is: Not {query}"

# Create knowledge base
knowledge_base = KnowledgeBase()

# Add rules
knowledge_base.add_rule(Rule("It is raining", "The streets are wet"))
knowledge_base.add_rule(Rule("The streets are wet", "You should drive slowly"))

# Add facts
knowledge_base.add_fact("It is raining")

# Create decision maker
decision_maker = DecisionMaker(knowledge_base)

# Make decision
print(decision_maker.make_decision("You should drive slowly"))
